# JAVA for 코딩 테스트

## 배열->리스트, 리스트->배열

![image-20210208114234557](md-images/image-20210208114234557.png)



## 진수변환

```java
int i = 127;
 
String binaryString = Integer.toBinaryString(i); //2진수
String octalString = Integer.toOctalString(i);   //8진수
String hexString = Integer.toHexString(i);       //16진수
 
System.out.println(binaryString); //1111111
System.out.println(octalString);  //177
System.out.println(hexString);    //7f
 
 
int binaryToDecimal = Integer.parseInt(binaryString, 2);
int binaryToOctal = Integer.parseInt(octalString, 8);
int binaryToHex = Integer.parseInt(hexString, 16);
 
System.out.println(binaryToDecimal); //127
System.out.println(binaryToOctal);   //127
System.out.println(binaryToHex);     //127
```



## String.toCharArray()

는 문자열을 한 글자씩 쪼개서
이를 char타입의 배열에 집어넣어주는 친절한 메소드이다.

- **String(문자열)**을 **char형 배열**로 바꾼다.

```java
  //how to use method
  String s1 = "Hello World";
  char[] charArr = s1.toCharArray();
```

- 추가로, **char형 배열**을 합쳐서 하나의 **String(문자열)**로 만들 수 있다.

```java
  //how to use method
  String s2 = new String(charArr);
```



## 대,소문자로 변경(문자열)

```java
String target = "abcdefg"; //대상 문자열
target = target.toUpperCase(); //대문자로 치환
```

```java
String target = "ABCDEFG"; //대상 문자열
target = target.toLowerCase(); //소문자로 치환
```

## 대,소문자로 변경(문자)

```java
Character.toUpperCase(c);
```





##  **문자 -> 숫자** 

### **String to Int**

가장 많이 사용한다고 생각됩니다.

자바 Integer클래스의 parseInt함수와 valueOf 함수로 변환 시켜줄 수 있습니다.

```java
//Integer.paseInt(String값)
//Integer.valueOf(String값)

String s_num = "10";
int i_num = Integer.parseInt(s_num); //String -> Int 1번방식
int i_num2 = Integer.valueOf(s_num); //String -> Int 2번방식
```



##  **숫자 -> 문자** 

### **Int to String**

자바 String클래스의 valueOf, toString 함수로 변환 시켜줄 수 있습니다.

```java
//String.valueOf(Int값)
//Integer.toString(Int값)

int i_num = 10;
String s_num;
		
s_num = String.valueOf(i_num); //문자 -> 숫자 1번방식
s_num = Integer.toString(i_num); //문자 -> 숫자 2번방식
s_num = ""+i_num; //문자 -> 숫자 3번방식
```