# MongoDB

---

## 특징 및 사용목적

- RDB의 한계 극복
  - 비정형 데이터 처리
  - 확장성
  - 속도
  - 트랙잭션 지원X

## 설계

- 함께 조회되는 겅우가 빈번한 데이터들은 같은 collection에 담아, query의 횟수를 줄일 수 있다
- 주로 읽기만 하는 데이터와 자주 업데이트 하는 데이터는 별개의 collection에 담는다

### Relation

- reference : 데이터를 정규화 / 잦은 수정 시 -> 쓰기가 빠르다
- embed : 데이터를 비정규화 / 통으로 조회 시 -> 읽기가 빠르다

|           | 장점                                           | 단점                                          |
| --------- | ---------------------------------------------- | --------------------------------------------- |
| Embed     | 읽기가 빠르고, 효율적(query 한 번에 모두 조회) | 수정이 비효율적(여러 document 중복 작업 필요) |
| Reference | 쓰기가 빠르고, 효율적(document 하나만 수정)    | 읽기가 비효율적(query를 여러번 실행)          |

---

## [설계](https://gamguma.dev/post/2022/04/mongodb_schema_design#설계)

### [One-to-One](https://gamguma.dev/post/2022/04/mongodb_schema_design#one-to-one)

------

**User**

```
{
    "_id": "ObjectId('mdkalsfmk2')",
    "nickname": "junseo",
    "campus": "42seoul",
}
```

위와 같은 `User document` 가 있을 때, `nickname` 이나 `campus` 와 같이 하나만 존재하는 값이 1:1 관계며, `key-value` 로 모델링 할 수 있습니다.

### [One-to-Few](https://gamguma.dev/post/2022/04/mongodb_schema_design#one-to-few)

------

**User**

```
{
    "_id": "ObjectId('mdkalsfmk2')",
    "nickname": "junseo",
    "campus": "42seoul",
    "projects": [
        { "name": "42WE", "isDone": false},
        { "name": "Decrypto", "isDone": true}
    ]
}
```

위와 같은 `User document` 에서 `projects` 의 타입은 배열이며 2개의 값을 가지고 있습니다. 이렇듯 `User document` 에서 `projects` 는 `One-to-Few` 관계입니다.

`One-to-Few` 처럼 몇 개의 데이터만 가지고 있을 경우엔 값을 `Embedding` 구조로 설계합니다.

### [One-to-Many 자식참조](https://gamguma.dev/post/2022/04/mongodb_schema_design#one-to-many-자식참조)

------

**User**

```
{
    "_id": "ObjectId('mdkalsfmk2')",
    "nickname": "junseo",
    "campus": "42seoul",
    "projects": [
        { "name": "42WE", "isDone": false},
        { "name": "Decrypto", "isDone": true}
    ],
    "creditCard": ["ObjectID('1234')", "ObjectID('4321')", "ObjectID('9399')"]
}
```

**Card**

```
{
    "_id": "ObjectId('4321')",
    "bank": "kakao",
    "isActive": "true",
    "accountNumber": "1234-56-7891234"
}
```

위의 `User document` 에서 `creditCard` 는 `Card` 스키마로 생성된 한 `Document` 를 참조하는 중입니다.

이처럼 한 유저가 여러 카드를 갖고 있으며 **따로 관리가 필요할 때**, **관계가 필요할 때** `One-to-Many` 구조로 설계합니다.

> 가능한 경우 `$lookup` 이나 `populate` 같은 `Join` 을 피하지만 이를 통해 더 나은 스키마 디자인 설계가 가능하다면 걱정하지 말고 사용하기!

### [One-to-Squillions 부모참조](https://gamguma.dev/post/2022/04/mongodb_schema_design#one-to-squillions-부모참조)

------

**ChatRoom**

```
{
    "_id": "ObjectId('4321')",
    "createdAt": ISODate("2021-04-28T09:42:41.382Z"),
    "users":"???",
}
```

**Chat**

```
{
    "_id": "ObjectId('328492489')",
    "chatRoom_id": "ObjectId('4321')", // 부모의 obj id 를 참조
    "createdAt": ISODate("2021-04-29T12:42:41.382Z"),
    "content":"피곤쓰",
}
```

이러한 채팅방, 채팅 스키마를 디자인할 때, `One-to-Many` 방식에서 `Embedding` 구조를 사용한다면, 채팅 데이터가 300개 넘어갔을 때 `Document` 의 **16mb 제한을 초과**해 버릴 것입니다. 더불어 `Referencing` 구조를 사용한다 하더라도 `ObjectID` 가 몇 천 개 쌓인다면 똑같이 용량 초과될 것입니다.

`One-to-Squillions` 구조를 사용한다면 채팅방의 `ObjectID` 로 해당 채팅방에서 주고받은 데이터를 쿼리 할 수 있게 되고, 용량 제한을 피하면서도 채팅방과 채팅의 관계를 유지시킬 수 있습니다.

---

mongodb에 트랜잭션 도입하기 : https://jh2021.tistory.com/24