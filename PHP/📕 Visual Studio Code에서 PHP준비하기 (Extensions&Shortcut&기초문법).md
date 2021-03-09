# 📕 Visual Studio Code에서 PHP준비하기 (Extensions&Shortcut&기초문법)

Visual Studio Code를 통해 php공부를 해보려 합니다. 가장 좋은 점은 Github와 연결이 된다는거죠😊
Github공부도 할 겸 Visual Studio Code로 PHP를 시작해보기로 하겠습니다.

## 📌 Extensions

먼저 PHP를 사용할 때 편리하게 코딩을 도와주는 extension들을 설치해줍니다.

-  

  PHP IntelliSense

  - PHP를 위한 고급 자동완성 및 리팩토링 지원
  - File > Preferences > Settings

```php
"php.validate.executablePath" : "C:/설치한 폴더/php.exe",
"php.validate.run" : "onType",
"php.validate.enable" : false
```

![img](https://media.vlpt.us/images/jiyoonoh-dev/post/c2dea99d-c6e4-416c-9007-383a9fba8d3b/image.png)

-  

  phpfmt- PHP formatter

  - 코드 정렬 지원(HTML 혼용 사용불가)
  - **shortcut** : shift + Alt + F

-  

  Format HTML in PHP

  - HTML이 혼용된 파일에서 HTML 영역을 선택, 마우스 우클릭하면 코드정렬

-  

  Auto Close Tag

  - HTML 닫기 태그를 자동으로 추가

-  

  Auto Rename Tag

  - HTML 태그명 자동으로 바꿔줌

-  

  ESLint

  - JavaScript 문법검사

-  

  Prettier

  - 대중적으로 쓰이는 Formatter
  - 저장할 때마다 자동으로 코드를 정렬해준다.
  - **beautify와 동시에 사용하면 충돌**
  - **기본 설정하기 :** 'Ctrl + ,' -> formatOnSave 검색 -> check

-  

  Beautify

  - 코드 들여쓰기를 정리해주는 확장기능
  - 설치 후 키 지정 필요
  - **기본 설정하기 :** 파일>기본설정>바로가기키> HookyQR.beautify 검색 후 단축키 지정

------

## 📖 VS Code 유용한 단축키

Tool을 처음 사용할 때 필수인 단축키도 알아봅시다! 더 많은 단축키는 keyboard Shortcut에서 확인하실 수 있어요 😊

- `Window`(`Mac`) : 내용

  ------

  `Ctrl(Cmd)` + `D` : 반복되는 코드를 한번에 수정
  `F2` : 변수명, 함수명 한번에 수정
  `Alt(opt)` + `↑ 또는 ↓` : 코드 위, 아래로 이동 (여러 줄도 가능해요)
  `Shift` + `Alt(opt)` + `↑ 또는 ↓` : 코드 위, 아래로 복사
  `Ctrl(Cmd)` + `/` : 주석처리, 주석해제
  `Alt(opt)` + 마우스 클릭 : 여러 곳에 커서 두고 수정 (위치 다를 때)
  `Ctrl(Cmd)` + `Alt(opt)` + `↑ 또는 ↓` : 여러 곳에 커서 두고 수정 (세로 위치 같을 때)
  `Shift` + `Alt(opt)` + `I` : 코드의 맨 마지막에 커서 두기
  `Shift` + `Alt(opt)` + 마우스 드래그 : 여러 줄을 커서 위치에 맞추어 박스 형태로 선택
  `Ctrl(Cmd)` + `Home 또는 End(↑ 또는 ↓)` + 마우스 드래그 : 코드 맨 위/아래로 이동
  `Ctrl(Cmd)` + `B` : 사이드바 숨김/표시

------

# 📕 PHP 시작하기

![img](https://media.vlpt.us/images/jiyoonoh-dev/post/794036c6-507d-4585-aa68-c58ba7709070/image.png)

구조를 먼저 알아볼게요!
Computer 내부에는 먼저 크게 Windows, Mac, Linux라는 **OS, 운영체제**가 있겠죵?
저의 모든 포스팅은 Window 기준으로 작성됩니다:)

운영체제 위에는 **Server**가 동작할거구요,
Server와 같은 위치, 혹은 그 위에 **PHP interpreter** 혹은 **PHP Engine**이 동작합니다!
여기서 PHP Engine은 php로 만들어진 코드를 해석해서 실행한 다음 Server와의 통신을 통해 돌려줍니다.
여기서의 'php로 만들어진 코드'가 php application이라고 불리는 .php파일입니다!

> #### 🧐 왜 Sever측 언어를 사용할까요? 
>
> 초창기에는 웹 서버와 웹 브라우저가 정보를 주고받는 아주 단순한 구조였습니다. 웹 브라우저가 **URL·URI**에 해당되는 웹 서버에게 웹의 정보를 요청하면, 웹 서버가 웹에 대한 정보가 담겨있는 **HTML(HyperText Markup Language)** 문서를 찾아 넘겨주고, 웹 브라우저는 그걸 보여주기만하면 끝나는거죠. 이 때, HTML 문서를 서버와 브라우저가 주고받기 위한 통신 규약을 **HTTP(HyperText Transper Protocol)** 라고 합니다. URL·URI는 HTML을 식별하는 식별자라고 할 수 있고, HTML이 편지라면 HTTP는 그 편지를 전송하기 위해 필요한 모든 것을 포함한다고 할 수 있습니다. 이 세가지를 유럽의 팀 버너스리 경이 개발한 인터넷의 3요소라고 합니다.
>
> 그런데 WEB이 성장을 하면서, 이 단순한 구조에 여러가지 문제들이 생깁니다. 예를 들면 Client가 Server에 어떤 글을 등록하고, 그 글을 여러 Client들이 봐야하는데, 그걸 Web Server 혼자서는 못한다는 문제가 있었어요. 그래서 그런 문제들을 해결하기 위해 고안된 방법으로, **CGI(Common Gateway Interface)** 라는 기술을 만들었습니다. 항상 Web server아래에서만 동작하는 PHP, Java, Python과 같은 **Server Side Script**가 생겼고, 이 Server Side Script와 Web Server가 통신할 수 있는 규약이 CGI입니다.
>
> 그렇게 앞 포스팅에서 설명했던 구동방식이 성립됩니다.😀
> ![img](https://media.vlpt.us/images/jiyoonoh-dev/post/5a55a57a-e404-44c1-a25b-0dac66a01e76/image.png)

## 📖 기초 문법

- ```
  <?php
  ```

   

  : php파일을 시작한다는 표시

  > ##### ⭐TIP : php.ini파일에 `short_open_tag = ON`으로 바꿔주면 php 생략가능 >> 설정파일을 변경하면 항상 Server는 재실행해줍니다.

- `?>` : php파일의 끝. 이후부터는 text로 보여지게 됩니다.

- `echo` : 데이터를 화면에 출력

- `;` : 명령 한 줄이 끝날 때마다 표시

  

### 주석 달기

> ##### ⭐TIP : 웹페이지의 개발자 도구에서 HTML의 주석은 보이지만, PHP의 주석은 보이지 않습니다. HTML에서 중요한 주석은 php의 시작과 끝 태그로 감싸서 사용합니다.
>
> ```php
> <?php /*<div>민감한 코드</div>*/?>
> ```

#### 🔹 한 문장 주석 달기

1) `#`
2) `//`

#### 🔹 여러 문장 주석 달기

```
/* */
```

### 간단한 실습

```php
<?php
  echo "Hello wolrd";
?>
```

위의 코드를 실행했을 때 php는 코드를 HTML형식으로 바꿔서 Server에 보내고,
Server는 웹 브라우저에 전달하여 웹브라우저는 아래의 HTML 코드를 실행하게 됩니다.
(참고 : [APM이란?](https://velog.io/@jiyoonoh-dev/APM이란))

```html
<html>
 <body>Hello world</body>
</html>
```

![img](https://media.vlpt.us/images/jiyoonoh-dev/post/c8642d6e-0bd8-475c-8de5-90fad8f7258e/image.png)

여기까지 Visual Studio Code로 PHP사용하기 위한 준비와 단축키, PHP구동방식, 기초사용법을 알아봤습니다!