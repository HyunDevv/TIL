# Python for 코딩 테스트

- 코딩 테스트 문제에서 시간제한은 통상 1 ~ 5초가량이다



## 자료형

- 정수형

  ```python
  a = 1000
  print(a)
  ```

- 실수형

  ```python
  a = 1000.
  a = -7.5
  print(a)
  ```
    - 지수 표현 방식

        1e9 = 10^9
      ```python
      INF = int(1e9)   # 보통 무한을 표기할 때 쓰인다
      print(INF) 
      ```
      
  - round() 함수

       ```python
       a = 0.3 + 0.6         # 0.89999999999
       print(round(a, 2))    # 0.9 (소수 셋째 자리에서 반올림)
       ```

  - 파이썬에서 나누기 연산자(/)는 나눠진 결과를 실수형으로 반환한다

       ```python
       print(7/3)       # 2.333333333335
       ```

  -  거듭제곱

       ```python
       print(5 ** 3)     # 125
       ```

- 복소수형

- 문자열

  - 문자열 안에 큰따옴표나 작은따옴표가 포함되어야 하는 경우

    ```python
    data = "Don't you know \"Python\"?"  # 백슬래쉬 사용
    # Don't you know "Python"?
    ```

    

- 리스트

  - 리스트의 원소에 접근할 때는 인덱스 값을 괄호에 넣습니다

    (인덱스틑 0부터 시작합니다)

  - 리스트의 인덱싱과 슬라이싱

  ```python
  a = [1,2,3,4,5,6,7,8,9]
  #    0 1 2 3 4 5 6 7 8
  #   -9-8-7-6-5-4-3-2-1
  print(a[2])        # 3
  print(a[-2])       # 7
  print(a[1:5])      # [2,3,4,5]    a[1]~a[4] 까지 출력됨!!
  
  n = 10
  a = [0] * n        # [0,0,0,0,0,0,0,0,0,0]
  print(a)
  ```

  - 리스트 컴프리헨션
  ```python
  array = [i for i in range(10)]
  print(array)       # [0,1,2,3,4,5,6,7,8,9]    
  
  # 0부터 19까지의 수 중에서 홀수만 포함하는 리스트
  array = [i for i in range(20) if i % 2 == 1]
  
  # 1부터 9까지의 수들의 제곱 값을 포함하는 리스트
  array = [i * i for i in range(1,10)]
  ```

  ```python
  # N*M 크기의 2차원 리스트 초기화!!!
  n = 4
  m = 3
  array = [[0] * m for _ in range(n)] # _는 i처럼 참조할 일이 없을 때 언더바로 사용!
  print(array)  # [[0,0,0],[0,0,0],[0,0,0],[0,0,0]]
  ```

  ![image-20201011130217417](md-images/image-20201011130217417.png)

  - 리스트에서 특정 값의 원소를 모두 제거하기

    ```python
    a = [1,2,3,4,5,5,5]
    remove_set = {3,5}
    result = [i for i in a if i not in remove_set]
    # [1,2,4]
    ```

    

- 튜플

  - 튜플은 한 번 선언된 값을 변경할 수 없습니다
  - 소괄호를 이용합니다

- 사전

  - 키와 값의 쌍을 데이터로 가지는 자료형

    ```python
    data = dict()
    data['사과'] = 'Apple'
    data['바나나'] = 'Banana'
    data['코코넛'] = 'Coconut'
    print(data)
    #{'사과': 'Apple','바나나': 'Banana','코코넛': 'Coconut'}
    ```

  - keys()

  - values()

- 집합 자료형

  - 중복허용x, 순서가 없다
  - 리스트 혹은 문자열을 이용해서 초기화 할 수 있다
    - set()함수 사용
    - 중괄호 안에 각 원소를 콤마를 기준으로 구분하여 삽입
  - 합집합 `a | b`
  - 교집합 `a & b`
  - 차집합 `a - b`
  - 원소추가 `add()`
  - 여러개 원소추가 `update( , )`
  - 특정 값을 가즌 원소 삭제 `remove()`



## 입출력

- input() : 한 줄의 문자열을 입력 받는 함수

- Map() :  리스트의 모든 원소에 각각특정한 함수를 적용할 때 사용

  - 공백을 기준으로 구분된 데이터를 입력 받을 때

    ```python
    # input().split()을 하면 문자열로 받는다!!
    
    list(map(int, input().split())) # 많이 입력 받을 때
    a,b,c =  map(int, input().split()) # 몇 개만 입력 받을 때
    ```

  -  2차원 배열을 입력 받을 때

    ```python
    '''
    3
    4
    0 0 0 0
    0 0 0 0
    0 0 0 0
    '''
    
    n = int(input())
    m = int(input())
    
    arr = []
    for i in range(n):
        arr.append(list(map(int, input().split())))
    ```

  - 빠르게 입력 받기 (입력값이 매우 큰 경우)

    ```python
    import sys
    
    data = sys.stdin.readline().rstrip()
    print(data)
    ```

  - print는 자동으로 줄 바꿈이 된다

    - print( 8, end=' ' )를 하면 줄 바꿈 대신 공백 하나를 하고 붙인다

    ```python
    print("정답은" + 7)   #오류
    print("정답은" + str(7))
    ```

    

##  조건문

- 파이썬에서는 **코드의 블록을 들여쓰기로 지정**

```python
a = 10

if a < 7:
    print("a")
elif a < 15:
    print("b")
else:
    print("c")
    print("d")       # 같이 실행!!..
    
   
print("끝")
```



- 비교연산자

- 논리연산자

  - X and Y
  - X or Y
  - not X

- 여러 개의 데이터를 담는 자료형을 위해 `in` 연산자와 `not in` 연산자가 제공된다

  - 리스트, 튜플, 문자열, 딕셔너리 모두 사용 가능

- pass

  ```python
  a = 10
  
  if a > 5:
      pass    # 나중에 작성할 코드 혹은 비워둘때
  else:
      print("else")
  ```

  

## 반복문

- while

  ```python
  i = 1
  result = 0
  
  # i가 9보다 작거나 같은 때 아래 코드를 반복적으로 실행
  while i <= 9:
      result += i
      i += 1
      
  print(result)
  ```

- for

  - range()의 인자를 하나만 넣으면 자동으로 시작 값은 0이 된다

  ```python
  result = 0
  
  # i는 1부터 9까지의 모든 값을 순회
  for i in range(1, 10):
      result += i
      
  print(result)
  ```

  ```python
  for i in range (1, 100, 3):   #3칸씩 띄면서 반복
      print(i)                  #1,4,7,10,...
  ```

  ```python
  scores = [90, 85, 77, 65, 97]
  cheating_student_list = {2,4}
  
  for i in range(5):
      if i + 1 in cheatng_student_list:
          continue
      if scores[i] >= 80:
          print(i + 1,"번 학생은 합격입니다.")
  ```

  

## 함수

```python
def add(a ,b):
	return a + b
	
print(add(3, 7))
```

```python
def add(a ,b):
	return a + b
	
print(add(b = 3,a = 7))
```

```python
a = 8

def func():
	global a     # a가져올 떄 사용 / 리스트는 global 필요없다
    a += 7
    
func()
print(a)
```



- 파이썬에서 함수는 여러 개의 반환 값을 가질 수 있다

```python
def operator(a, b):
    return a+b, a-b, a*b, a/b

a, b, c, d = operator(3, 7)
```

## 람다

> 함수를 매우 간단하게 작성할 수 있다

```python
print((lambda a, b: a + b)(3, 5))
```

```python
list1 = [1,2,3,4,5]
list2 = [6,7,8,9,10]

result = list(map(lambda a, b: a + b, list1, list2)) 
print(result)               # [7,9,11,13,15]
```



![image-20201013221631110](md-images/image-20201013221631110.png)

<img src="md-images/image-20201013221842800.png" alt="image-20201013221842800" style="zoom:50%;" />

![image-20201013221919584](md-images/image-20201013221919584.png)

![image-20201013222006018](md-images/image-20201013222006018.png)

![image-20201013222147757](md-images/image-20201013222147757.png)

![image-20201013222203663](md-images/image-20201013222203663.png)

![image-20201013222242484](md-images/image-20201013222242484.png)