# Git

> Git은 **분산형 버전관리시스템(DVCS)** 중 하나이다.



## Git 사전 준비

 #### 1. [Github](https://github.com/) 가입

* 이메일 인증을 해야한다

#### 2. [git bash (git for windows)](https://gitforwindows.org/) 다운

#### 3.[GitHub Student Developer Pack](https://education.github.com/pack) 받기

* @edu @ac.kr 이메일이 있으면(대학교), 무료로 한단계 높은 버전 제공
* 다른 이메일 등록하신 분들도 추가로 하실 수가 있다.



---

> git을 사용하기 전에 커밋을 남기는 사람에 대한 정보를 설정(최초)    
>
> *  {여기안에는 변수를 쓴다} 

```bash
$ git config --global user.name '{username}'
$ git config --global user.email '{email}' 
```

* 추후에 commit을 하면, 작성한 사람(author)로 저장된다.

* email 정보는 github에 등록된 이메일로 설정을 하는 것을 추천 (잔디밭)

* 설정 내용을 확인하기 위해서는 아래의 아래의 명령어를 입력한다.

  ```bash
  $ git config --global -l
  user.name=KimJaeHyun52
  user.email=kjhkjh5265@smail.kongju.ac.kr
  ```



## 기초흐름

> 작업->add->commit
>
> ![image-20200917194529265](md-images/image-20200917194529265.png)



### 0. 저장소 설정

```bach
$ git init
Initialized empty Git repository in C:/Users/Master/Desktop/test2/.git/
```

* git 저장소를 만들게 되면 해당 디렉토리 내에 `.git/` 폴더가 생성
* git bach에서는 `(master)` 로 현재 작업중인 브랜치가 표기 된다.

## 1. `add`

> 커밋을 위한 파일 목록(staging area)

```bash
$ git add .          # 현재 디렉토리의 모든 파일 및 폴더
$ git add a.txt      # 특정 파일
$ git add md-images/ # 특정 폴더
```

## 2. `commit`

> **버전**을 기록(스냅샷)

```bash
$ git commit -m '커밋메시지'
```

* 커밋 메시지는 현재 버전을 알 수 있도록 명확하게 작성한다.
* 커밋 이력을 남기기 확인하기 위해서는 아래의 명령어를 입력한다.

```bash
$ git log
$ git log -1 # 최근 한개의 버전
$ git log --oneline # 한줄로 간단하게 표현
$ git log -1 --oneline
```

## status - 상태 확인

> git에 대한 모든 정보는 status에서 확인할 수 있다.

```bash
$ git status
# master 브랜치에 있다
On branch master

No commits yet
  # unstage를 하기 위해서.... 명령어
  # working directory 단계
Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
        new file:   a.txt
# 트래킹 x 파일들
# git으로 아직 관리를 x
# working directory 단계
Untracked files:
  (use "git add <file>..." to include in what will be committed)
        b.txt

```

![image-20200917132253857](md-images/image-20200917132253857-1600332273391.png)





## 원격 저장소 활용하기

> 원격 저장소를 제공하는 서비스는 github, gitlab, bitbucket 등이 있다.

### 1. 원격 저장소 사용하기

```bash
$ git remote add origin {URL}
```

* 깃아, 원격(remote)저장소로 추가해줘(add) origin이라는 이름으로 URL을

  * origin 자리에는 remote의 이름이 들어가며 관례 상 origin을 사용한다.

* 원격저장소 삭제하기 위해서는 아래의 명령어를 사용한다.

  ```bash
  $ git remote rm origin
  ```

  

### 2. 원격 저장소 확인하기

```bash
$ git remote -v
origin  https://github.com/KimJaeHyun52/TIL.git (fetch)
origin  https://github.com/KimJaeHyun52/TIL.git (push)
```

### 3. push

```bash
$ git push origin master
```

