### PHP - Windows + nginx + PHP7 + MariaDB 서버구축

긍정곰 2017. 10. 5. 22:36



**※본 글은 지극히 개인적으로 참고하기위한 글로써 해요체 등의 존대는 쓰지 않으며, 설명이 부실할수 있습니다. 음슴체나 반말어투에 거부감이 있으신분은 다른자료를 참고하시길 권합니다. 그외에 내용의 설명이 부족하여 궁금한점이 있을경우 질문을 주시면 제가 아는 한도내에서 답변을 드리겠습니다.**

이전에 해둔 윈도우 서버에 먼지만 쌓여가던 찰나에 다시 꺼내어 쓸일이 있어서 아래와 같이 셋팅 메뉴얼을 남겨둔다.

추신. httpd아파치와 php7의 연계성이 영 좋지 못하기때문에(라이브러리 충돌 및 오류)앞으로는 nginx를 서버 클라이언트로 활용하고 php자체 cgi로 연동하는 방식으로 서버 구축을 하는것이 좋을듯하다.(대세가 바뀌지 않는 한은...)

아래는 필요한 유틸리티들의 공식홈페이지 및 다운로드 주소.

**서버 클라이언트 nginx**

[nginx 공식홈페이지(https://nginx.org/)](https://nginx.org/)

참고사항 : 대체 가능한 방안으로는 httpdApache와 IIS를 활용한 방법이 있으나 httpd는 라이브러리 충돌의 문제가 있고, IIS는 윈도우를 비싼제품(프로페셔널 이상 버젼의 윈도우, 윈도우 자체 기능이므로...)을 사용해야 이용할수 있는 기능이기에 nginx를 적극 권장함.

**PHP for Windows**

[PHP for Windows 공식홈페이지(http://windows.php.net/)](http://windows.php.net/)

참고사항1 : 윈도우용버젼을보면 Thread Safe(쓰레드 세이프)와 Non Thread Safe(논 쓰레드 세이프)로 나뉘는데 쓰레드 세이프 버젼을 권장한다.(해당 글은 쓰레드 세이프 버젼을 기준으로 한다)

참고사항2 : PHP for Windows의 경우 실행을 위해 비주얼 스튜디오 재배포 패키지를 설치해야한다. 해당 환경구성이 되어있지 않을 경우에는 vcruntime140.dll 파일이 없다면서 에러를 내뿜는데 그럴 경우 하단의 주소에서 내려받거나 혹은 비주얼 스튜디오를 따로 설치해주면 된다.(비주얼 스튜디오 커뮤니티 에디션은 2013 버젼부터 개인사용자는 무료이기때문에 해당 에디션을 받아서 설치하면 된다.)

비주얼 스튜디오 재배포 패키지 내려받기 - https://www.microsoft.com/ko-kr/download/details.aspx?id=48145

비주얼 스튜디오 내려받기 - https://www.visualstudio.com/ko/downloads/

그외 : 보통 비주얼 스튜디오 런타임 관련 에러를 보면 vcruntimexxx.dll 등으로 표기되는데 xxx란의 숫자에 따라 어느버젼의 비주얼 스튜디오의 재배포 패키지가 필요한가 달라지게 된다.

해당 종속성을 가지기 시작한것은 비주얼스튜디오 2003부터 인데(년도 넘버링을 붙이고 C#을 지원하면서 부터이다.)뒷자리 숫자에 따른 해당 비주얼 스튜디오 버젼은 아래와 같다.

```
Visual Studio 2003 - vcruntime70.dll
Visual Studio 2005 - vcruntime80.dll
Visual Studio 2008 - vcruntime90.dll
Visual Studio 2010 - vcruntime100.dll
Visual Studio 2012 - vcruntime110.dll
Visual Studio 2013 - vcruntime120.dll
Visual Studio 2015 - vcruntime140.dll
Visual Studio 2017 - vcruntime150.dll
```

MSVCRxxx.dll, MSVCPxxx.dll도 마찬가지.

**데이터 베이스 MariaDB**

[MariaDB 공식홈페이지(https://mariadb.org/)](https://mariadb.org/)

참고사항 : msi로 설치해서 쓸수있는 버젼과 zip 압축파일로 제공되는 무설치 버젼이 제공되는데 이글에서는 무설치 버젼을 기준으로 설명한다.

그외 : MySQL을 이용할수도 있으나 MySQL AB(MySQL 개발사)가 썬마이크로시스템즈(이 회사는 JAVA로 유명하다)에 인수되었었는데 이후에 썬마이크로시스템즈가 오라클에 인수합병되면서 MySQL도 같이 오라클에 흡수되었다. 여전히 무료로 제공되고있기는 하지만 논란의 여지는 충분히 있기때문에 마리아DB의 사용을 적극 권장함.

**nginx 설정**

nginx를 압축을 풀어준뒤 안에 살펴보면 conf 라는 이름의 폴더가 있다.

여기안에 들어가면 nginx.conf 라는 파일이 존재하는데, 이것을 메모장 같은 문서작성 프로그램으로 연다.

그럼 아래와 같이 뜨는데...

```
#user  nobody;
worker_processes  1;

#error_log  logs/error.log;
#error_log  logs/error.log  notice;
#error_log  logs/error.log  info;

#pid        logs/nginx.pid;


events {
    worker_connections  1024;
}


http {
    include       mime.types;
    default_type  application/octet-stream;

    #log_format  main  '$remote_addr - $remote_user [$time_local] "$request" '
    #                  '$status $body_bytes_sent "$http_referer" '
    #                  '"$http_user_agent" "$http_x_forwarded_for"';

    #access_log  logs/access.log  main;

    sendfile        on;
    #tcp_nopush     on;

    #keepalive_timeout  0;
    keepalive_timeout  65;

    #gzip  on;

    server {
        listen       80;
        server_name  localhost;

        #charset koi8-r;

        #access_log  logs/host.access.log  main;

        location / {
            root   html;
            index  index.html index.htm;
        }

        #error_page  404              /404.html;

        # redirect server error pages to the static page /50x.html
        #
        error_page   500 502 503 504  /50x.html;
        location = /50x.html {
            root   html;
        }

        # proxy the PHP scripts to Apache listening on 127.0.0.1:80
        #
        #location ~ \.php$ {
        #    proxy_pass   http://127.0.0.1;
        #}

        # pass the PHP scripts to FastCGI server listening on 127.0.0.1:9000
        #
        #location ~ \.php$ {
        #    root           html;
        #    fastcgi_pass   127.0.0.1:9000;
        #    fastcgi_index  index.php;
        #    fastcgi_param  SCRIPT_FILENAME  /scripts$fastcgi_script_name;
        #    include        fastcgi_params;
        #}

        # deny access to .htaccess files, if Apache's document root
        # concurs with nginx's one
        #
        #location ~ /\.ht {
        #    deny  all;
        #}
    }


    # another virtual host using mix of IP-, name-, and port-based configuration
    #
    #server {
    #    listen       8000;
    #    listen       somename:8080;
    #    server_name  somename  alias  another.alias;

    #    location / {
    #        root   html;
    #        index  index.html index.htm;
    #    }
    #}


    # HTTPS server
    #
    #server {
    #    listen       443 ssl;
    #    server_name  localhost;

    #    ssl_certificate      cert.pem;
    #    ssl_certificate_key  cert.key;

    #    ssl_session_cache    shared:SSL:1m;
    #    ssl_session_timeout  5m;

    #    ssl_ciphers  HIGH:!aNULL:!MD5;
    #    ssl_prefer_server_ciphers  on;

    #    location / {
    #        root   html;
    #        index  index.html index.htm;
    #    }
    #}

}
```

뭔가 길지만 직접 수정해줘야 하는 부분은 별거없다.

여기서 nginx 설정의 문법을 조금 짚고 넘어가야한다.

nginx의 설정문서에서 #(Sharp)기호는 주석을 의미한다.

즉 앞에 #이 붙어있으면 해당 구문은 실행하지 않는다는 의미를 가진다.

대부분이 앞에 #이 붙어있는데 해당 부분들은 지금은 일단 실행하지 않는 설정으로 되어있다는 이야기.

그리고 fastcgi_param SCRIPT_FILENAME 항목에 경로를 수정해주어야 한다.

경로는 웹페이지들이 들어갈 경로를 그대로 써주면 되는데 예를 들어 C드라이브에 nginx 폴더안에 html폴더안에 웹페이지들이 들어간다면 아래와 같이 해주면 된다.

```
fastcgi_param  SCRIPT_FILENAME  C:/nginx/html$fastcgi_script_name;
```

우리가 해줄려는 것은 php cgi의 연동이기때문에 해당 부분의 주석을 지워주는 것과 스크립트 경로 지정만 해주면 설정은 다 끝난것이나 다름없다.

아래와 같이 되어있는 부분을...

```
...
        # pass the PHP scripts to FastCGI server listening on 127.0.0.1:9000
        #
        #location ~ \.php$ {
        #    root           html;
        #    fastcgi_pass   127.0.0.1:9000;
        #    fastcgi_index  index.php;
        #    fastcgi_param  SCRIPT_FILENAME  /scripts$fastcgi_script_name;
        #    include        fastcgi_params;
        #}
...
```

아래와 같이 바꿔준다.

```
...
        # pass the PHP scripts to FastCGI server listening on 127.0.0.1:9000
        #
        location ~ \.php$ {
            root           html;
            fastcgi_pass   127.0.0.1:9000;
            fastcgi_index  index.php;
            fastcgi_param  SCRIPT_FILENAME  C:/nginx/html$fastcgi_script_name;
            include        fastcgi_params;
        }
...
```

이렇게 하면 우선 nginx의 설정은 끝이다.

출력되는 웹페이지들이 들어갈 경로는 기본적으로 nginx 폴더에 html 이라는 폴더로 설정되어있다.(이곳에 사용하는 웹페이지들을 넣어주면 된다)

추가 설정

index.php 파일명 주소창에 표시되지 않게 하기.

(http://www.pblab.kr/index.php 라고 하지 않고 http://www.pblab.kr 이라고 입력해도 index.php파일로 연결되고 주소창에는 표시되지 않게 해준다.)

```
...
        #access_log  logs/host.access.log  main;

        location / {
            root   html;
            index  index.html index.htm index.php;
        }

        #error_page  404              /404.html;
...
```

볼드표기된 index.php 부분을 위와 같이 추가해준다.

이렇게 해주면 주소창에 굳이 index.php라고 넣지 않더라도 index.html이나 index.htm처럼 자동으로 연결해준다.

**PHP 설정**

내려받은 PHP의 압축을 풀면 php.ini-development라는 파일이 있을것이다.

이것을 php.ini로 변경해준다. 확장자명 변경에 대한 안내가 나오면 그대로 확인을 눌러서 변경을 확정하면 된다.

기본적인 설정으로는 데이터베이스 연동이 막혀있기때문에 확장자를 변경해준 php.ini를 에디터를 통해(에디터 툴이 없다면 아주 훌룡한 윈도우 메모장을 쓰자)일부 내용을 수정해준다.

먼저 확장기능 dll들의 경로를 지정해준다.

```
; Directory in which the loadable extensions (modules) reside.
; http://php.net/extension-dir
; extension_dir = "./"
; On windows:
; extension_dir = "ext"
extension_dir = "C:\php7\ext"
```

주석을 지우고 디렉터리 설정을 해줘도 되고 위에처럼 그냥 한줄 추가해줘도 된다.

디렉터리 설정을 따로 해주지 않을경우 기본설정된 경로는 C:/php/ext 가 된다.(C드라이브 안에 php 폴더안에 php파일들이 있을경우 따로 설정해줄 필요가 없다.)

그리고 추가로 확장기능중 어떤걸 사용할지 설정해줘야 하는데...

```
;;;;;;;;;;;;;;;;;;;;;;
; Dynamic Extensions ;
;;;;;;;;;;;;;;;;;;;;;;
```

라고 되어있는 부분에 조금 내려보면 이런 구문들이 있다.

```
;extension=php_bz2.dll
extension=php_curl.dll
;extension=php_fileinfo.dll
;extension=php_gd2.dll
;extension=php_gettext.dll
;extension=php_gmp.dll
;extension=php_intl.dll
;extension=php_imap.dll
;extension=php_interbase.dll
;extension=php_ldap.dll
extension=php_mbstring.dll
;extension=php_exif.dll      ; Must be after mbstring as it depends on it
extension=php_mysqli.dll
;extension=php_oci8_12c.dll  ; Use with Oracle Database 12c Instant Client
extension=php_openssl.dll
;extension=php_pdo_firebird.dll
extension=php_pdo_mysql.dll
;extension=php_pdo_oci.dll
;extension=php_pdo_odbc.dll
;extension=php_pdo_pgsql.dll
;extension=php_pdo_sqlite.dll
;extension=php_pgsql.dll
;extension=php_shmop.dll
```

**여기서 사용할 확장기능은 앞에 세미콜론을 지워서 주석처리를 풀어준다.**

마리아 DB(혹은 MySQL)를 사용할려면 extension=php_mysqli.dll 의 주석을 풀어주어야 사용가능하다.

오래된 자료들을 보면 extension=php_mysql.dll 뒤에 i가 안붙은 그냥 dll이 있으나, 지금 7버젼에는 해당 dll이 더이상 지원되지 않는지 확장기능 리스트에도 들어가있지 않으므로 그냥 위에 하나만 풀어주면 된다.

그리고 extension=php_pdo_mysql.dll PDO(PHP Data Object)확장 기능은 사용한다면 주석을 풀어주고 아니면 그대로 두어도 상관은 없다.

**Maria DB 설정**

압축을 원하는 곳에 풀어준다.

그리고 명령 프롬프트를 관리자 권한으로 실행하여 아래와 같이 입력해준다.(여기서는 C드라이브에 MariaDB라는 폴더에 압축을 풀어준것으로 가정하고 설명한다.)

```
C:\MariaDB\bin\mysql_install_db --datadir=C:\MariaDB\data --service=MariaDB --port=3306
```

이렇게 하면 윈도우 서비스 항목에 MariaDB라는 이름으로 등록이 되는데 확인할려면 아래와 같이 메뉴를 찾아 들어가면 확인할수 있다.

제어판 - 시스템 및 보안 - 관리 도구에 "서비스" 항목을 열어서 확인할수있다.

상황에 따라 명령프롬프트에 입력되어야할 구문이 틀려지는데 이를테면 포트를 3306이 아닌 다른포트를 사용할려면 끝에 포트 항목의 번호를 변경해주면되고 서비스 등록이름을 다르게 하고 싶다면 --service 항목의 이름을 바꿔주면된다.

이제 서비스 등록이 되었기때문에 윈도우의 서비스 도구를 열어서 등록된 서비스의 상태 확인 및 중지 상태일경우 시작을 여기서 시켜주면 DB의 온오프를 간편하게 할수있게 된다.

**서버 구동**

전반적인 설정이 다 되었다면 이제 구동을 해봐야할 차례이다.

우선 아래의 방식은 개인적으로 권장하는 형태이며 꼭 아래와 같이 할필요는 없다.

서비스 등록된 MariaDB의 서비스 "시작" -> php-cgi 실행 -> nginx 실행

\1. 서비스 등록된 MariaDB의 서비스 "시작" 말 그대로이므로 윈도우의 서비스 도구를 열어서 MariaDB 항목을 찾고 거기서 "시작"이라고 보이면 그냥 눌러주면된다.

만약 "시작"이 안보이고 "일시중지" "중지"만 보인다면 이미 실행되고 있는 상태이므로 딱히 손댈필요가 없다.

\2. php-cgi 실행 명령 프롬프트를 열고 아래와 같이 입력한다.(굳이 관리자 권한이 아니더라도 상관없다. 여기서는 C드라이브에 php7 폴더에 압축파일을 풀어둔것으로 가정한다.)

```
C:\php7\php-cgi -b 127.0.0.1:9000 -c php.ini
```

주의할점은 명령프롬프트를 종료하면 백그라운드로 실행이 되지 않기때문에 같이 종료되어버린다.(명령프롬프트창을 닫으면 안된다.)

\3. nginx 실행 명령 프롬프트를 열고 아래와 같이 입력한다.(굳이 관리자 권한이 아니더라도 상관없다. 여기서는 C드라이브에 nginx 폴더에 압축파일을 풀어둔것으로 가정한다.)

우선 아래와 같이 입력하여 nginx 폴더로 이동한다.

```
cd C:\nginx
```

그러고 난뒤에 아래와 같이 입력한다.

```
nginx
```

주의 할점은 php-cgi와 달리 명령프롬프트창을 닫더라도 계속해서 실행이 된다는 점인데 클라이언트의 재시작이나 종료가 필요할때가 있을것이다.

그때는 위와 같이 nginx폴더로 이동한 상태에서 아래와 같이 입력하여 nginx를 재시작 혹은 종료시킬수 있다.

재시작을 하고자 할때는...

```
nginx -s reload
```

종료를 시키고자 할때는...

```
nginx -s stop
```

**테스트**

아래는 DB커넥션 테스트를 위한 코드이다.

dbcontest.php

```
<?php
$s = mysqli_connect("localhost", "루트계정", "비밀번호") or die("실패입니다");
print "성공입니다";
mysqli_close($s);
?>
```



"루트계정", "비밀번호"는 자신이 DB설치시에 설정했던 계정과 비밀번호를 넣으면된다.

만약 따로 설정하지 않았다면 디폴트는 "root", "" 이다.

성공입니다.

라고 뜰경우 DB와 정상적으로 통신이 가능한것이고 실패입니다 라고 뜰경우 설정을 다시 점검해볼필요가 있다.



출처: https://pblab.tistory.com/22 [긍정곰의 연구소]

출처: https://pblab.tistory.com/22 [긍정곰의 연구소]