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

