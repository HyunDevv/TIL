윈도우10 64bit 환경 아파치(Apache) 설치하기



**1. https://www.apachelounge.com/download/ 에 접속하여 다운로드합니다.**



![img](https://t1.daumcdn.net/cfile/tistory/2469B43458B63ACD05)





**2. 다운받은 파일의 압축을 풉니다.**

**
**

![img](https://t1.daumcdn.net/cfile/tistory/2563BA3758B63B921F)





**Apache24 폴더를 C:\ 폴더로 이동시켜줍니다. 이동시킨 후 최종 경로는 C:\Apache24 경로가 됩니다.**



![img](https://t1.daumcdn.net/cfile/tistory/2569663758B63C5E21)





**3. 환경설정**



![img](https://t1.daumcdn.net/cfile/tistory/251A803E58B63D322F)



**httpd.conf 파일을 메모장으로 엽니다.**

**기본적으로 아래 부분을 찾아서 설정값을 내 설치 PC에 맞게 변경합니다.**



![img](https://t1.daumcdn.net/cfile/tistory/2230523F58B63E9A07)



**Server Root 경로를 지정합니다. 위에서 C:\Apache24로 지정했기 때문에 맞게 수정합니다. C: 다음에 '/' 역슬래시로 표시합니다.**



![img](https://t1.daumcdn.net/cfile/tistory/2352B53F58B63E9E05)



**Listen : 웹 서버의 포트를 설정합니다. 기본 값은 80입니다. 다른 포트번호를 사용하지 않는다면 그대로 둡니다.**



![img](https://t1.daumcdn.net/cfile/tistory/26547F3F58B63EA033)



**웹브라우저로 웹 서버에 접속했을 때 보여지는 웹사이트의 파일들이 저장되는 경로입니다.**

**http://localhost:80 (또는 http://localhost)로 접속했을 때 DocumentRoot 내의 index.html 페이지를 찾아서 보여줍니다.**





**4. 아파치 (Apache) 설치하기**



**관리자모드로 명령프롬프트 창을 실행합니다.**

![img](https://t1.daumcdn.net/cfile/tistory/2438133C58B641D82F)



**명령프롬프트창에서 c:\Apache24/bin 경로로 이동하여 설치파일을 실행합니다.**

**
**

**c:\Apache24/bin**

**
**

**httpd.exe -k install**



![img](https://t1.daumcdn.net/cfile/tistory/2575273858B642C012)



**주의: 만약 "vcruntime140.dll 파일이(가) 없어 프로그램을 시작할 수 없습니다. 프로그램을 다시 설치하여 이 문제를 해결하십시오." 라는  메시지창이 뜨면서 설치가 안되는 경우는 아래 URL을 접속하여 해결방안을 참조하세요.** 

**
**

**http://ldcc.tistory.com/326**



**설치한 아파치 서버를 삭제하고 싶으면 httpd.exe -k uninstall 명령어를 입력하시면 됩니다.**





**5. 아파치 (Apache) 웹서버 실행하기**



**윈도우 탐색기에서 아래 파일을 실행합니다.**

**C:\Apache24\bin\ApacheMonitor.exe**



![img](https://t1.daumcdn.net/cfile/tistory/217FCF3558B645EB25)





**윈도우 오른쪽 하단 작업표시줄에 아파치 아이콘 > 마우스 우측버튼 클릭 후 아파치 모니터를 실행합니다.**

![img](https://t1.daumcdn.net/cfile/tistory/2554373F58B6471013)



**아파치 모니터에서 start와 stop버튼으로 서버를 실행시키고 중지시킵니다.**

![img](https://t1.daumcdn.net/cfile/tistory/2701F53F58B6476A12)





**6. 실행 확인**



**웹 브라우저를 실행하여 http://localhost/로 접속합니다. 아래 페이지가 뜨면 정상적으로 아파치 웹 서버 설치가 완료됩니다.**



![img](https://t1.daumcdn.net/cfile/tistory/2738944258B647ED2D)





이상으로 기본적인 아파치 (Apache) 웹 서버 설치 과정을 살펴봤습니다. 

httpd.conf 파일에는 많은 설정 옵션이 있으니 검색이나 관련 서적을 통해 더 많은 설정 과정을 살펴보시기 바랍니다.



출처: https://kiwinote.tistory.com/75 [KiwiSoft]