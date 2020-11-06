# AWS EC2 Linux 사용하기

1. AWS 계정 생성 및 콘솔 로그인

[https://aws.amazon.com/ko/free/](https://aws.amazon.com/ko/free/?all-free-tier.sort-by=item.additionalFields.SortRank&all-free-tier.sort-order=asc)





2. 지역 서울로 변경

![img](https://cafeptthumb-phinf.pstatic.net/MjAyMDExMDJfMjQ3/MDAxNjA0MzA3NDA1MDMz.R1p9PAFflVQ87cutLhaCXvPS8tv7lK4Ag7OzKVaM1hEg.EbiBrrFdQLw-a0xwOFUwv8mGeuEE6k_tavPHhMfENPcg.PNG/image.png?type=w1600)





3. EC2 인스턴스 생성 & Linux 2 설치

https://docs.aws.amazon.com/ko_kr/AWSEC2/latest/UserGuide/EC2_GetStarted.html

EC2 Linux 인스턴스 시작하기



- 보안의 인바운드 규칙 - 보안그룹 - SSH/TCP/22/모든곳  설정할것! 

![image-20201106194517045](C:%5CUsers%5CMaster%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20201106194517045.png)

- 키의 권한설정 확인하기!

![image-20201106195038472](C:%5CUsers%5CMaster%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20201106195038472.png)





4. GUI 설치 및 접속 (+웹브라우저 설치)

https://aws.amazon.com/ko/premiumsupport/knowledge-center/ec2-linux-2-install-gui/

- Windows Server 2019 및 Windows 10의 최신 버전 - OpenSSH는 설치 가능한 구성 요소로 포함되어 있습니다. 자세한 내용은 [Windows의 OpenSSH](https://docs.microsoft.com/en-us/windows-server/administration/openssh/openssh_overview)를 참조하십시오.

  - 윈도우 - 앱 및 기능 - 선택적 기능 - OpenSSH 확인!

  ![image-20201106200401441](C:%5CUsers%5CMaster%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20201106200401441.png)



5. vncviewer 설치

![image-20201106200006047](C:%5CUsers%5CMaster%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20201106200006047.png)

---

이후 과정은 VMware 환경의 처음 설정 과정과 같음



5. JDK 1.8 설치

https://cafe.naver.com/multiiot2020/565

접근 권한 부족할 경우 **sudo** 사용하여 진행

sudo cp -r jdk1.8.0 /usr/local    // "sudo" 붙여서 진행



6. Eclipse 2020-06 설치

https://www.eclipse.org/downloads/download.php?file=/oomph/epp/2020-06/R/eclipse-inst-linux64.tar.gz



7. eclipse.ini 수정 (필)

이클립스 설치 경로에 있는 eclipse.ini 파일 수정

vi /home/ec2-user/eclipse/java-2020-06/eclipse/eclipse.ini

-vm (jdk 경로) . . . -Xms256m -Xmx256m

![img](https://cafeptthumb-phinf.pstatic.net/MjAyMDExMDJfMTMy/MDAxNjA0MzEwNjcyNjc3.II1pL1dylmWDGYtqMS0Tvp14ZjtWkLRuVEY2WSjovKEg.DjfdY41ciOw5cn6heuC1v5LFQFXcFVvjnu2_GIMe7x8g.PNG/image.png?type=w1600)