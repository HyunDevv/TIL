# Sequelize : nodejs ORM

---

## 개요

ORM(Object-Relational Mapping)은 객체지향 패러다임을 활용하여 관계형 데이터베이스(RDB)의 데이터를 조작하게 하는 기술이다. 이를 활용하면 쿼리를 작성하지 않고도 객체의 메서드를 활용하는 것처럼 쿼리 로직을 작성할 수 있다. 백엔드를 구축하다가 RDB에 단순쿼리를 날리는 것이 비효율적이라 생각되어 찾아보던 도중 Node.js의 대표적인 ORM인 Sequelize를 보게 되었고 이참에 사용법을 정리해보고자 한다. Sequelize는 MySQL, PostgreSQL, MariaDB 등 많은 RDBMS를 지원하고 Promise 기반으로 구현되었기 때문에 비동기 로직을 편리하게 작성할 수 있다.

## 설치 및 초기화

이 포스팅에선 MySQL과 Sequelize를 사용하여 간단한 CRUD 작업을 해보기로 한다. 따라서 그에 맞는 패키지들을 설치해주어야 한다.

```
yarn init -y
yarn add mysql2 sequelize
yarn add global sequelize-cli
```

기본 패키지들을 설치해주고 CLI를 사용해서 여러 작업들을 수행하기 위해 글로벌로 패키지를 설치한다. 이제 초기화를 하자.

```
sequelize init
```

초기화를 진행하면 아래와 같은 폴더 및 파일들이 생긴다.

```
.
|-- README.md      
|-- config
|   `-- config.json
|-- migrations     
|-- models
|   `-- index.js   
|-- package.json   
|-- seeders        
`-- yarn.lock
```

- **config** : 데이터베이스 설정 파일, 사용자 이름, DB 이름, 비밀번호 등의 정보 들어있다.
- **migrations** : git과 비슷하게, 데이터베이스 변화하는 과정들을 추적해나가는 정보로, 실제 데이터베이스에 반영할 수도 있고 변화를 취소할 수도 있다.
- **models** : 데이터베이스 각 테이블의 정보 및 필드타입을 정의하고 하나의 객체로 모은다.
- **seeders** : 테이블에 기본 데이터를 넣고 싶은 경우에 사용한다.

이제 각 폴더 및 파일들에 대해 알아보도록 하자.

## 설정

데이터베이스 관련 설정 파일인 `config.json` 이 있다. 여기선 로컬 MySQL을 사용하기로 하고 `instagram` 란 이름의 데이터베이스를 생성해보자. 나의 경우 아이디/비밀번호 모두 `root` 이다.

```
mysql -uroot -p # 입력하고 비밀번호 입력
create database instagram;
use instagram;
```

데이터베이스를 생성하고 선택하자. 이제 이 과정들에 대한 정보들을 `config.json` 에 적어주면 되는데 `development` , `test` , `production` 이 있기 때문에 모두 수정해준다 치고 여기선 하나만 수정해보자.

```
"development": {
  "username": "root",
  "password": "root",
  "database": "instagram",
  "host": "127.0.0.1",
  "dialect": "mysql",
  "operatorsAliases": false
}
```

## 모델 생성해서 데이터베이스에 반영하기

Sequelize CLI를 통해서 모델을 생성할 수 있고 마이그레이션을 통해 실제 데이터베이스에 반영할 수 있다. `User` 라는 모델을 생성해서 이 작업을 해보자.

```
sequelize model:generate --name User --attributes user_id:integer,user_name:string
```

모델을 생성하는 명령어이며 이를 통해 2가지 파일이 생성된다.

- `model/user.js`

```
'use strict';
module.exports = (sequelize, DataTypes) => {
  const User = sequelize.define('User', {
    user_id: DataTypes.INTEGER,
    user_name: DataTypes.STRING
  }, {});
  User.associate = function(models) {
    // associations can be defined here
  };
  return User;
};
```

모델에 있는 필드들의 타입을 정의하고 각 모델간의 관계를 설정하는 `associate` 부분이 있다.

- `migrations/[타임스탬프]-create-user.js`

```
'use strict';
module.exports = {
  up: (queryInterface, Sequelize) => {
    return queryInterface.createTable('Users', {
      id: {
        allowNull: false,
        autoIncrement: true,
        primaryKey: true,
        type: Sequelize.INTEGER
      },
      user_id: {
        type: Sequelize.INTEGER
      },
      user_name: {
        type: Sequelize.STRING
      },
      createdAt: {
        allowNull: false,
        type: Sequelize.DATE
      },
      updatedAt: {
        allowNull: false,
        type: Sequelize.DATE
      }
    });
  },
  down: (queryInterface, Sequelize) => {
    return queryInterface.dropTable('Users');
  }
};
```

마이그레이션 파일이 타임스탬프 접미사와 같이 생성되고 `id` , `createdAt` , `updatedAt` 필드가 자동으로 생성된다. 여기서 `up` 프로퍼티는 실제 DB에 적용되는 부분이고 `down` 은 이 작업을 취소할 때이다. 여기선 `user_id` 를 primary key로 사용할 것이고 `createdAt` 과 `updatedAt` 이 필요없으니 이쪽을 수정해줘야 한다.

```
'use strict';
module.exports = {
  up: (queryInterface, Sequelize) => {
    return queryInterface.createTable('Users', {
      user_id: {
        allowNull: false,
        autoIncrement: true,
        primaryKey: true,
        type: Sequelize.INTEGER
      },
      user_name: {
        type: Sequelize.STRING
      }
    });
  },
  down: (queryInterface, Sequelize) => {
    return queryInterface.dropTable('Users');
  }
};
```

단, 이렇게 하면 모델 부분도 `primaryKey` 를 수정해줘야 하고 `timestamps` 옵션도 추가해줘야 한다.

```
'use strict';
module.exports = (sequelize, DataTypes) => {
  const User = sequelize.define('User', {
    user_id: {
      type: DataTypes.INTEGER,
      primaryKey: true
    },
    user_name: DataTypes.STRING
  }, {
    timestamps: false
  });
  User.associate = function(models) {
    // associations can be defined here
  };
  return User;
};
```

이제 실제 DB에 반영해보자.

```
sequelize db:migrate
```

MySQL CLI에서 확인하면 테이블이 만들어진 것을 확인할 수 있다.

```
desc users;
+-----------+--------------+------+-----+---------+----------------+
| Field     | Type         | Null | Key | Default | Extra          |        
+-----------+--------------+------+-----+---------+----------------+        
| user_id   | int          | NO   | PRI | NULL    | auto_increment |        
| user_name | varchar(255) | NO   |     | NULL    |                |        
+-----------+--------------+------+-----+---------+----------------+
```

마이그레이션을 취소할 수도 있는데 이전 명령어에 `undo` 만 붙여주면 된다.

```
sequelize db:migrate:undo
```

## CRUD

생성된 `Users` 테이블에 CRUD를 수행해보자. Sequelize는 이에 관한 많은 메서드들을 제공하며 이를 활용하면 간단하게 할 수 있다.

### 모델 불러오기

모델을 사용해서 쿼리를 수행하기 때문에 해당 파일을 불러와서 사용해야 한다. 루트에 `index.js` 를 만들고 여기서 사용하자.

```
const models = require("./models");
```

### Create (사용자 생성)

```
models.User.create({
  user_name: "John"
}).then(_ => console.log("Data is created!"));
```

DB를 확인해보면 들어갔음을 알 수 있다.

```
+---------+-----------+
| user_id | user_name |
+---------+-----------+
|       1 | John      |
+---------+-----------+
```

### Read (사용자 조회)

```
models.User.findAll().then(console.log);
```

콘솔을 확인해보면 결과가 나온다.

```
Executing (default): SELECT `user_id`, `user_name` FROM `Users` AS `User`;
[
  User {
    dataValues: { user_id: 1, user_name: 'John' },
    ....
  }
]
```

### Update (사용자 수정)

수정할 부분을 먼저 찾아야 하기 때문에 여기 `findOne` 을 사용하고 그 다음 `update` 를 수행한다.

```
models.User.findOne({ where: { user_name: "John" }})
.then(user => {
  if (user) {
    user.update({ user_name: "Bob" })
    .then(r => console.log("Data is updated!"));
  }
});
```

DB를 확인해보면 John에서 Bob으로 바뀌었다는 걸 확인할 수 있다.

```
+---------+-----------+
| user_id | user_name |
+---------+-----------+
|       1 | Bob       |
+---------+-----------+
```

### DELETE (사용자 삭제)

```
models.User.destroy({ where: { user_name: "Bob" }})
.then(_ => console.log("Data was deleted!"));
```

DB를 확인해보면 데이터가 없어졌다는 걸 알 수 있다.

```
Empty set
```

이렇게 CRUD 관련한 사용법을 알아봤는데 이외에도 수많은 메서드들이 존재한다. 공식문서를 살펴보면 다양하게 나와있지만 좀 더 편하게 읽기 위해서 [Velog의 Sequelize 번역시리즈](https://velog.io/@cadenzah/series/Sequelize-API-Document) 를 추천한다.

## 기존 DB에서 모델 추출하기

내 프로젝트의 경우 기존에 테이블을 모두 만들어놓았기 때문에 ORM을 사용하기 위해선 이걸로부터 모델을 만들어야 했다. 하지만 Sequelize 자체에선 해당 기능을 제공하지 않았고 [sequelize-auto](https://github.com/sequelize/sequelize-auto) 에서 제공하고 있었다. 따라서 이를 활용했다. 시연해보기 위해 MySQL에서 SQL로 테이블을 만들어보자.

```
create table photos(photo_id int not null auto_increment, photo_url varchar(100) not null, primary key(photo_id));
+-----------+--------------+------+-----+---------+----------------+
| Field     | Type         | Null | Key | Default | Extra          |        
+-----------+--------------+------+-----+---------+----------------+        
| photo_id  | int          | NO   | PRI | NULL    | auto_increment |        
| photo_url | varchar(100) | NO   |     | NULL    |                |        
+-----------+--------------+------+-----+---------+----------------+
```

추출하기 전에 혼동을 줄이기 위해 기존의 `models` 폴더에서 `index.js` 를 제외한 모든 파일들을 삭제하자. 이제 sequelize-auto를 사용해서 모델을 추출하는데, 나는 글로벌로 설치를 했다. 로컬로 설치해서 package.json 스크립트로 추가해 사용해도 무방하다. sequelize-auto의 추출 명령어는 좀 긴데, 옵션만 이해하면 직관적이다.

```
sequelize-auto -o "./models" -d instagram -h localhost -u root -p 3306 -x root -e mysql
```

`-o` 는 결과물 경로, `-d` 는 DB 이름, `-h` 는 호스트 이름, `-u` 는 사용자, `-p` 는 포트, `-x` 는 비밀번호, `-e` 는 데이터베이스 종류이다. 실행하면 `users` , `photos` 테이블에 대한 모델이 추출된다.

```
models
|-- index.js
|-- photos.js
`-- users.js
```

이제 이를 활용하여 DB를 다룰 수 있게 된다.

## 마무리

지금까지 Node.js의 대표적인 ORM 패키지인 Sequelize의 기초를 살펴보았다. 보통은 공식 문서를 살펴보는 것이 가장 빠르지만 그리 친절하지 않은 것 같아서 구글링이 더욱 효과적이라고 생각한다. 기존의 일반적인 쿼리 방식에 비해 Sequelize가 갖는 장점은 객체지향 프로그래밍 방식에 익숙한 우리들에게 좀 더 효율적인 데이터 조작을 가능하게 해주는데 있다. 또한 SQL을 작성할 때 실수하는 부분들을 걱정할 염려가 없으니 굉장히 편리하다. 프로젝트의 크기가 매우 크다면 성능이슈에 대해 고려할 부분이 있겠지만 현재 시점에선 RDB를 다룰 때는 Sequelize가 필수일 정도로 반드시 익혀둬야 한다고 생각한다. 여기서 작성한 모든 코드는 [깃헙](https://github.com/baeharam/sequelize-codelab) 에 있다.

## 참고

- [Velog, Sequelize CLI를 사용하여 User API 만들기](https://velog.io/@jeff0720/Sequelize-CLI를-사용하여-간단한-User-API-만들기-vdjpb8nl0k)
- [Sequelize 사용하기](https://jongmin92.github.io/2017/04/08/Node/sequelize/)
- [Sequelize 공식문서](https://sequelize.org/v5/)

---

출처 : 

https://baeharam.netlify.app/posts/Node.js/Node.js-Sequelize-%EB%8B%A4%EB%A3%A8%EA%B8%B0