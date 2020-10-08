R 

온라인교재:https://thebook.io/006723/



데이터 분석 - R, 파이썬 분석

​	- 파이썬은 소프트웨어적인 접근이 더많고 + **AI**

​	- R은 **통계학 적 접근** - 마케팅,리서치



- 가트너의 빅데이터 3V 모델
  - Volume
  - Velocity
  - Variety          +   2V

통계학자들이 R 라이브러리를 계속 만들면서 발전하고 있다



- R의 단점
  - 속도가 느리다
  - 데이터 분석에만 특화 되있다, 대규모 IT서비스 개발에 접목이 어렵다
  - 문제 발생 시 스스로 해결해야 한다



- R 라이브러리 위치
  - C:\Program Files\R\R-3.5.1\library



## 데이터 타입



### 변수 이름 규칙

> R의 변수명은 알파벳, 숫자, _(언더스코어), .(마침표)로 구성되며, -(하이픈)은 사용할 수 없다. 첫 글자는 **알파벳 또는 .으로 시작**해야 한다. 만약 .으로 시작한다면 . 뒤에는 숫자가 올 수 없다. 예를 들어, 다음은 모두 올바른 변수명이다.

### 변숫값 할당

- 변수에 값을 할당할 때는 `<-` 를 사용



할당 연산자 중 = 는 명령의 최상위 수준에서만 사용

아래 상황에서 = 를 사용하면 x에 값이 저장되지 않는다.

```
  > mean(x = c(1, 2, 3))
  [1] 2
  > x
  Error: object 'x' not found
  >
```



- R 변수
  - 스칼라
  
  - 벡터
  
  - 리스트
  
  - 행렬
  
  - 배열
  
  - 데이터 프레임
  
    

### 스칼라

> 스칼라란 **단일 차원의 값**을 뜻하는 것으로 숫자 1, 2, 3, …을 예로 들 수 있다. 반면 좌표 평면 위에 있는 점인 (1, 2)는 2차원 값이므로 이 절에서 설명하는 스칼라에 해당하지 않는다.

> R에서 데이터 타입의 기본은 벡터Vector다. 따라서 스칼라 데이터는 길이가 1인 벡터(즉, 길이가 1인 배열)와 같은 것으로 볼 수 있다.

#### NA(Not Available)

>  데이터 값이 없음을 뜻한다.

```R
is.na(
	x # R의 데이터 객체
)
```

#### NULL

>  NULL은 NULL 객체를 뜻하며, 변수가 초기화되지 않았을 때 사용한다. NULL은 NA와 구분해서 생각해야 한다. 어떤 변수에 NULL이 저장되어 있는지는 is.null( )을 사용해 판단할 수 있다.

| is.null : 변수에 NULL이 저장되어 있는지를 판단한다.          |
| ------------------------------------------------------------ |
| `is.null(   x  # R의 데이터 객체  )`반환 값은 NULL이 저장되어 있으면 TRUE, 그렇지 않으면 FALSE다. |

#### 문자열

#### 진리값

> TRUE, FALSE 대문자로 사용한다

#### 팩터

> 팩터Factor는 범주형Categorical 데이터(자료)를 표현하기 위한 데이터 타입이다.

```
> sex <- factor("m", c("m", "f"))
# m과 f중에 m이 들어간다
> sex
[1] m
Levels: m f
```

- 여러개의 값 중에 하나가 들어간다 

### 벡터(배열과 같다)

> 벡터Vector는 다른 프로그래밍 언어에서 흔히 접하는 배열의 개념으로, 한 가지 스칼라 데이터 타입의 데이터를 저장할 수 있다.

- R의 벡터는 슬라이스Slice를 제공한다. 슬라이스란 배열의 일부를 잘라낸 뒤 이를 또 다시 배열처럼 다루는 개념을 뜻한다.
- 또한, **벡터의 각 셀에는 이름을 부여할 수 있다.** 따라서 벡터에 저장된 요소들을 색인을 사용하여 접근하는 것뿐 아니라 이름을 사용해서도 접근할 수 있다. 이런 특징을 사용하면 데이터를 좀 더 의미 있는 형태로 저장할 수 있다.

| c : 주어진 값들을 모아 벡터를 생성한다.                      |
| ------------------------------------------------------------ |
| `c(   ...  # 벡터로 모을 R 객체들 )`반환 값은 벡터다.        |
| names : 객체의 이름을 반환한다.                              |
| `names(   x  # 이름을 얻어올 R 객체  )`반환 값은 x와 같은 길이의 문자열 벡터 또는 NULL이다. |
| names<- : 객체에 이름을 저장한다.                            |
| `names(   x          # 이름을 저장할 R 객체  ) <- value # 저장할 이름` |

```R
 v1 <- c(1,2,3) # 3행으로 들어간다
names(v1) <- c("d1","d2","d3")

v1[1,3]       # 오류
v1[c(1,3)]    # 1,3번째 값이 출력됨

v1["d1"]
v1[c("d1","d3")]
length(v1)    # 3
NROW(v1)      # 3   /  소문자는 행렬에서만 사용
names(v1)[2]  # "d2"
```

| identical : 객체가 동일한지를 판단한다.                      |
| ------------------------------------------------------------ |
| `identical(   x,  # R 객체    y   # R 객체 )`반환 값은 x와 y가 동일하면 TRUE, 그렇지 않으면 FALSE다. |
| union : 합집합을 구한다.                                     |
| `union(   x,  # 벡터    y   # 벡터  )`반환 값은 x와 y의 합집합이다. |
| intersect : 교집합을 구한다.                                 |
| `intersect(   x,  # 벡터    y   # 벡터  )`반환 값은 x와 y의 교집합이다. |
| setdiff : 차집합을 구한다.                                   |
| `setdiff(   x,  # 벡터    y   # 벡터  )`반환 값은 x와 y의 차집합이다. |
| setequal : x와 y가 같은 집합인지 판단한다.                   |
| `setequal(   x,  # 벡터    y   # 벡터  )`반환 값은 x와 y가 같은 집합인지 여부다. |

| 연산자       | 의미                                                         |
| :----------- | ------------------------------------------------------------ |
| value %in% x | 벡터 x에 value가 저장되어 있는지 판단함                      |
| x + n        | 벡터 x의 모든 요소에 n을 더한 벡터를 구함. 마찬가지로 *, /, -, == 등의 연산자를 적용 가능함 |

v2 <- v1 + 10

```
> seq(3, 7)     # 1씩 증가
[1] 3 4 5 6 7
> seq(7, 3)     # 1씩 감소
[1] 7 6 5 4 3
> seq(3, 7, 2)  # 2씩 증가
[1] 3 5 7
> seq(3, 7, 3)  # 3씩 증가
[1] 3 6
```

```
> 3:7
[1] 3 4 5 6 7
> 7:3
[1] 7 6 5 4 3
```

| rep : 주어진 값을 반복한다.                                  |
| ------------------------------------------------------------ |
| `rep(   x,      # 반복할 값이 저장된 벡터    times,  # 전체 벡터의 반복 횟수    each    # 개별 값의 반복 횟수  )`반환 값은 반복된 값이 저장된 x와 같은 타입의 객체다. |

### 리스트 (해시 테이블와 비슷)(k,v)

> 자료 구조 책에서 리스트List는 배열과 비교할 때 데이터를 중간 중간에 삽입하는 데 유리한 구조로 설명한다.

```
> (x <- list(name="foo", height=70))
$ name
[1] "foo"

$ height
[1] 70
```

```
list1 <- list(v1 = "data1", v2 = "data2") # =으로 써야함!!

> list1$v1
[1] "data1"

> list1[v1]
$<NA>
NULL
```

### 행렬(동일타입의 2차원 Matrix)

> R의 행렬Matrix은 수학 시간에 배운 행렬의 정의와 같이 행(로우), 열(컬럼)의 수가 지정된 구조다. 벡터와 마찬가지로 행렬에는 **한 가지 유형의 스칼라만 저장**할 수 있다.

```
> matrix(c(1, 2, 3, 4, 5, 6, 7, 8, 9), nrow=3)
     [,1] [,2] [,3]
[1,]    1    4    7
[2,]    2    5    8
[3,]    3    6    9
```

```
> matrix(c(1, 2, 3, 4, 5, 6, 7, 8, 9), nrow=3, byrow=TRUE)
     [,1] [,2] [,3]
[1,]    1    2    3
[2,]    4    5    6
[3,]    7    8    9
```

| nrow : 배열의 행의 수를 구한다.                              |
| ------------------------------------------------------------ |
| `nrow(   x  # 벡터, 배열 또는 데이터 프레임 )`반환 값은 x의 행의 수다. |
| ncol : 배열의 열의 수를 구한다.                              |
| `ncol(   x  # 벡터, 배열 또는 데이터 프레임 )`반환 값의 x의 열의 수다. |
| dim : 객체의 차원 수를 구한다.                               |
| `dim(   x  # 행렬, 배열 또는 데이터 프레임 )`반환 값은 x의 차원 수다. |

### 배열(다차원 행렬)

> 행렬이 2차원 데이터라면 배열Array은 다차원 데이터다.

### 데이터 프레임(다중(데이터타입) 행렬)

데이터 프레임Data Frame은 처리할 데이터를 마치 엑셀의 스프레드시트와 같이 표 형태로 정리한 모습을 하고 있다. 데이터 프레임의 각 열에는 관측값의 이름이 저장되고, 각 행에는 매 관측 단위마다 실제 얻어진 값이 저장된다. 예를 들어, 다음 성적 데이터와 같은 모습이 데이터 프레임에 저장되는 데이터의 전형적인 예다.

| 성명   | 국어 | 영어 |
| ------ | ---- | ---- |
| 홍길동 | 80   | 94   |
| 김길동 | 97   | 100  |
| 박길동 | 85   | 97   |

이처럼 자연스럽게 데이터를 표현하는 데이터 타입이기 때문에 데이터 프레임은 R에서 가장 중요한 데이터 타입이며, 많은 R 함수에서 인자로 데이터 프레임을 받는다.

 *data.frame( )에 문자열 벡터를 지정할 때 stringsAsFactor를 지정하지 않으면 문자열이 팩터로 바뀌는 것과는 다른 점이다.*

```
> (d <- data.frame(x=c(1, 2, 3, 4, 5),
+                   y=c(2, 4, 6, 8, 10),
+                   z=c('M', 'F', 'M', 'F', 'M')))
   x  y  z
1  1  2  M
2  2  4  F
3  3  6  M
4  4  8  F
5  5 10  M
```

```
> d$w <- c("A", "B", "C", "D", "E")
> d              # 새로운 열이 추가됨!
   x  y  z  w
1  6  2  M  A
2  7  4  F  B
3  8  6  M  C
4  9  8  F  D
5 10 10  M  E
```

| 문법               | 의미                                                         |
| ------------------ | ------------------------------------------------------------ |
| d$colname          | 데이터 프레임 d의 컬럼 이름 colname에 저장된 데이터          |
| d[m, n, drop=TRUE] | 데이터 프레임 d의 m행 n 컬럼에 저장된 데이터.m과 n을 벡터로 지정하여 다수의 행과 컬럼을 동시에 가져올 수 있으며 m, n에는 색인뿐만 아니라 행 이름이나 컬럼 이름을 지정할 수 있다.만약 m, n 중 하나를 생략하면 모든 행 또는 컬럼의 데이터를 의미한다.d[, n]과 같이 행을 지정하지 않고 특정 컬럼만 가져올 경우 반환 값은 데이터 프레임이 아니라 해당 컬럼의 데이터 타입이 된다. **이러한 형 변환을 원하지 않으면 drop=FALSE를 지정하여 데이터 프레임을 반환하도록 할 수 있다.** |

#### 유틸리티 함수

데이터를 살펴보기 위한 유틸리티 함수

| head : 객체의 처음 부분을 반환한다.                          |
| ------------------------------------------------------------ |
| `head(  x,    # 객체  n=6L  # 반환할 결과 값의 크기 )`반환 값은 x의 앞부분을 n만큼 잘라낸 데이터다. |
| tail : 객체의 뒷부분을 반환한다.                             |
| `tail(  x,    # 객체  n=6L  # 반환할 결과 값의 크기 )`반환 값은 x의 뒷부분을 n만큼 잘라낸 데이터다. |
| View : 데이터 뷰어를 호출한다.                               |
| `View(  x,     # 데이터 프레임으로 강제 형 변환한 뒤 뷰어로 볼 데이터  title  # 뷰어 윈도우의 제목 )` |

### 타입판별

데이터 타입 판별 함수

| 함수             | 의미                                     |
| ---------------- | ---------------------------------------- |
| class(x)         | 객체 x의 클래스                          |
| str(x)           | 객체 x의 내부 구조                       |
| is.factor(x)     | 주어진 객체 x가 팩터인가                 |
| is.numeric(x)    | 주어진 객체 x가 숫자를 저장한 벡터인가   |
| is.character(x)  | 주어진 객체 x가 문자열을 저장한 벡터인가 |
| is.matrix(x)     | 주어진 객체 x가 행렬인가                 |
| is.array(x)      | 주어진 객체 x가 배열인가                 |
| is.data.frame(x) | 주어진 객체 x가 데이터 프레임인가        |

### 타입 변환

데이터 타입 변환 함수

| 함수             | 의미                                        |
| ---------------- | ------------------------------------------- |
| as.factor(x)     | 주어진 객체 x를 팩터로 변환                 |
| as.numeric(x)    | 주어진 객체 x를 숫자를 저장한 벡터로 변환   |
| as.character(x)  | 주어진 객체 x를 문자열을 저장한 벡터로 변환 |
| as.matrix(x)     | 주어진 객체 x를 행렬로 변환                 |
| as.array(x)      | 주어진 객체 x를 배열로 변환                 |
| as.data.frame(x) | 주어진 객체 x를 데이터 프레임으로 변환      |

---

## 엑셀파일 불러오기

콘솔에서 (readxl 패키지를 설치!)

```
install.packages("readxl")
```

스크립트에서

```R
library(readxl)
ex1 <- read_excel("엑셀파일주소")
str(ex1)
```

`read_excel()` 사용!



## TXT,CSV 파일 불러오기

- 구분자가 `,` 로 되어있는 경우

```R
ex1 <- read.table("price.csv",
                   sep = ",",
                   header = T,
                   fill = T   # 결측값을 NA로 채워준다!!
                  )
str(ex1)
```

`read.table` 사용!



한글 컨트롤이 예민하다..

- encoding / fileEncoding



외부에서 가져오면 typeof로 꼭 데이터구조 확인한다!!

(데이터프레임이 아닐 수 도 있다.)



CSV 파일 입출력 함수

| read.csv : CSV 파일을 데이터 프레임으로 읽어들인다.          |
| ------------------------------------------------------------ |
| `read.csv(  file,          # 파일명                                                            header=FALSE,  # 파일의 첫 행을 헤더로 처리할 것인지 여부  # 데이터에 결측치가 포함되어 있을 경우 R의 NA에 대응시킬 값을 지정한다.  # 기본값은 "NA"로, "NA"로 저장된 문자열들은 R의 NA로 저장된다.  na.strings="NA",  # 문자열을 팩터로 저장할지 또는 문자열로 저장할지 여부를 지정하는 데 사용한다. 별다른  # 설정을 하지 않았다면 기본값은 보통 TRUE다.  stringsAsFactors=default.stringsAsFactors() )`반환 값은 데이터 프레임이다. |
| write.csv : 데이터 프레임을 CSV로 저장한다.                  |
| `write.csv(  x,              # 파일에 저장할 데이터 프레임 또는 행렬             file="",        # 데이터를 저장할 파일명  row.names=TRUE  # TRUE면 행 이름을 CSV 파일에 포함하여 저장한다. )` |



- `.rda` 파일은 R만 아는 파일이다



## 필요할 때 추가해서 사용하는 패키지

> 로드,가공,시각화,모델링,리포트,공간 등 다양한 기능을 가진 패키지를 사용할 수 있다.

- 위치 :C:\Users\i\Documents\R\win-library\3.5
- 컴퓨터 간 동일한 패키지 환경 만들기 : 위의 경로의 폴더를 복사해 사용하면 된다.
- But, 리눅스와 같은 다른 OS에서 사용하려면 리눅스에서 다시 설치해야 한다.



### dplyr 패키지

> 데이터를 가공할 때 변수명을 변경하거나 필요한 데이터를 추출하는 기능 등

install.packages("dplyr")

library(dplyr)



- filter() 함수: 조건식에 맞는 데이터를 필터링

  - filter(데이터 세트, 조건절)

- arrange() 함수 : 정렬 (기본 오름차순)

  - arrange(데이터 세트, 정렬할 열1, desc(정렬할 열2))

- select() 함수 : 지정한 변수만 추출

  - select(데이터 세트, 추출 열)

- mutate() 함수 : 데이터 세트에 열을 추가

  - mutate(데이터 세트, 추가할 열 이름 = 조건1,...)

- distinct() 함수 : 중복 값을 제거

  - distinct(데이터 세트, 열1, 열2, ..)

- summarise() 함수 : 통계 함수와 함께 사용, 데이터를 요약

  - summarise(데이터 세트, 요약 결과 저장 열 = 통계 함수)

- group_by() 함수

  - group_by(데이터, 묶을 열)

    ```R
    # mtcars에서 cyl별로 묶고 갯수를 나타낼 때
    gr_crl <- group_by(mtcars, cyl)
    summarise(gr_cyl, n())
    ```

- sample_n() 함수 : 데이터에서 샘플 데이터를 추출

  - sample_n(데이터 세트, 추출할 랜덤샘플 개수)

- sample_frac() 함수

  - sample_frac(데이터 세트, 추출할 랜덤샘플 비율)



- `%>%` 연산자

  > `%>%` 연산자는 파이프, 즉 연결하여 연산하는 기능

  ```R
  #mtcar에서 cyl별 그룹으로 묶고 갯수(n())로 요약
  group_by(mtcars, cyl) %>% summarise(n())
  ```

  



- rename() 함수 : 컬럼이름 바꾸기


```R
library(dplyr)  #dplyt 라이브러리 설치
sh <- read.csv("shop2.txt",
               header = T,
               stringsAsFactors=F,
               fileEncoding = "UTF-8"
)
sh <- rename(sh, ID=TX_ID, NAME=TX_NM, AGE=TX_A, TEMP=TX_T,PRICE=TX_P, QT=TX_Q)
#rename 사용가능(A, B=C) A에서 C를 B로 바꾼다 
```

---

sh2 <- sh %>% select(-ID,-AGE,-GRADE)
sh3 <- sh %>% filter(GRADE == 'G' & AGE_HL == 'M' & TEMP != 'NA')
mean(sh3$TOTAL)
sh4 <- sh %>% arrange(desc(AGE), MM)



smr <- sh %>% summarise(TOT = sum(PRICE), AGES = mean(AGE))
smr2 <- sh %>% group_by(NAME) %>% summarise(TOTAVG = mean(PRICE * QT))          #List
smr3 <- as.data.frame(smr2)

---

- ifelse를 3항연산자 처럼 사용

  ```R
  sh$AGE_NY <- ifelse(sh$AGE >= 25, "Y", "N")
  ```

---



### psych 패키지

install.packages("psych")

library(psych)

- describe()



### descr 패키지

install.packages("descr")

library(descr)

- freq() 함수



- names(airquality) <- tolower(names(airquality)) : 컬럼명을 모두 소문자로 바꾸는 함수

---



### reshape2 패키지

install.packages("reshape2")

library(reshape2)

- melt() 함수 : 가로정렬 함수이다 (167p 참조)
  melt (데이터 세트, id.var = "정렬 할 기준열", measure.vars = "변환(보고싶은) 열")

| 기준열 | variable (반환열) | value (값) |
| :----: | :---------------: | :--------: |
|  ...   |        ...        |    ...     |
|  ...   |        ...        |    ...     |

- dcast() 함수 : melt 반대로 - variable을 컬럼으로..(172p 참조)

  - dcast(데이터 세트, 기준열1 + 기준열2 ~ 변환열(variable))

  - dcast(데이터 세트, 기준열1 + 기준열2 ~ 변환열(variable), 처리함수(ex.mean))



- acast() 함수 : dcast() 함수와 비슷하지만 형태가 다르다 
  - acast(데이터 세트, 기준열1 + 기준열2 ~ 변환열(variable))
  - acast(데이터 세트, 기준열1 + 기준열2 ~ 변환열(variable), 처리함수(ex.mean))



### rJava 패키지

### KoNLP 패키지

> KoNLP와 wordcloud2를 통해 형태소를 분석하고 다양한 모양의 워드클라우드를 만들 수 있다.

#### 설치

1. rstudio 끄기

아래 사이트에서 Rtools35.exe 설치

설치 시 기본 옵션이외의 설치 옵션 모두 클릭

https://cran.r-project.org/bin/windows/Rtools/history.html

2. rstudio 켜기

install.packages("multilinguer")

3. 의존성 설치

install.packages(c("hash", "tau", "Sejong", "RSQLite", "devtools", "bit", "rex", "lazyeval", "htmlwidgets", "crosstalk", "promises", "later", "sessioninfo", "xopen", "bit64", "blob", "DBI", "memoise", "plogr", "covr", "DT", "rcmdcheck", "rversions"), type = "binary")

4. Git를 통해 KoNLP를 다운 받기 

\- git 연결 프로그램 다운로드

install.packages("remotes")

\- KoNLP 설치

remotes::install_github('haven-jeon/KoNLP', upgrade = "never", INSTALL_opts=c("--no-multiarch"))

5. KoNLP 설치 확인 및 단어 다운로드

library(KoNLP)

useSystemDic()

useSejongDic()

useNIADic()

6. install.packages("wordcloud2")



텍스트 수집 -> 분해 -> 단어 추출 -> 정제 -> 정형 데이터 생성 -> 분석 -> 시각화

- wordcloud2 사용 (wc.txt라는 있는 자료로 분석)

```R
#시작전에 wc.txt에 분석할 문서를 넣는다
library(KoNLP)
library(wordcloud2)
useSystemDic()
useSejongDic()
useNIADic()

#새로운 단어들을 추가한다
add_wd <- c("코로나","코로나19")
buildDictionary(user_dic = data.frame(
  add_wd, rep("ncn",length(add_wd))
), replace_usr_dic =  T)

wd <- readLines("wc.txt", encoding = "UTF-8")
#이 문장에서 명사만 추출하겠다
wd2 <- sapply(wd, extractNoun, USE.NAMES =  F) # USE.NAMES =  F열이름을 사용하지 않겠다) 


# 추출한 명사들을 벡터로 만든다
lwd <- unlist(wd2)

# 사전에서 단어를 제외한다
lwd <- gsub("[0-9]","",lwd)
lwd <- gsub("[a-z]","",lwd)
lwd <- gsub("[A-Z]","",lwd)
lwd <- gsub("\\W","",lwd)
lwd <- gsub("","",lwd)
lwd <- gsub("한국","",lwd)
lwd <- gsub("유엔","",lwd)

# 벡터데이터를 필터링한다(x는 단어들이 하나씩 들어간다)
lwd2 <- Filter(function(x){
  nchar(x) >= 2  #한 자리의 단어는 제외한다
},lwd)

# 벡터안에서 단어들을 센다
wc <- table(lwd2)

# 제일 많은 순으로 정렬
wc <- sort(wc, decreasing = T)

# wordcloud2로 그린다
my_graph <- wordcloud2(wc, color = "random-light", backgroundColor = "black")

# html형식으로 temp.html 파일 저장하기
library("htmlwidgets")
saveWidget(my_graph,"tmp.html",selfcontained = F)

#temp.html 파일 → fig_1.png로 변환하기
library(webshot)
webshot::install_phantomjs()
webshot("tmp.html","fig_1.png", delay =5, vwidth = 720, vheight=720) 


```

- 웹사이트 자료 분석

  ```R
  #시작전에 wc.txt에 분석할 문서를 넣는다
  library(KoNLP)
  library(wordcloud2)
  useSystemDic()
  useSejongDic()
  useNIADic()
  
  #새로운 단어들을 추가한다
  add_wd <- c("코로나","코로나19")
  buildDictionary(user_dic = data.frame(
    add_wd, rep("ncn",length(add_wd))
  ), replace_usr_dic =  T)
  
  wd <- readLines("https://www.nongmin.com/news/NEWS/FLD/CNT/327519/view", encoding = "UTF-8")
  #이 문장에서 명사만 추출하겠다
  wd2 <- sapply(wd, extractNoun, USE.NAMES =  F) # USE.NAMES =  F열이름을 사용하지 않겠다) 
  
  
  # 추출한 명사들을 벡터로 만든다
  lwd <- unlist(wd2)
  
  # 사전에서 단어를 제외한다
  lwd <- gsub("[0-9]","",lwd)
  lwd <- gsub("[a-z]","",lwd)
  lwd <- gsub("[A-Z]","",lwd)
  lwd <- gsub("\\W","",lwd)
  lwd <- gsub("","",lwd)
  lwd <- gsub("창열","",lwd)
  lwd <- gsub("__","",lwd)
  lwd <- gsub("_","",lwd)
  
  
  # 벡터데이터를 필터링한다(x는 단어들이 하나씩 들어간다)
  lwd2 <- Filter(function(x){
    nchar(x) >= 2  #한 자리의 단어는 제외한다
  },lwd)
  
  # 벡터안에서 단어들을 센다
  wc <- table(lwd2)
  
  # 제일 많은 순으로 정렬 후 상위 100개만 저장
  wc <- head(sort(wc, decreasing = T),100)
  
  # wordcloud2로 그린다
  my_graph <- wordcloud2(wc, color = "random-light", backgroundColor = "black")
  
  # html형식으로 temp.html 파일 저장하기
  library("htmlwidgets")
  saveWidget(my_graph,"tmp.html",selfcontained = F)
  
  #temp.html 파일 → fig_1.png로 변환하기
  library(webshot)
  webshot::install_phantomjs()
  webshot("tmp.html","c:/R/fig_1.png", delay =5, vwidth = 720, vheight=720) 
  ```

  