# FTP 설치

P669 - FTP 설치

1. vsftpd 설치

yum  -y  install  vsftpd



2. systemctl  restart   vsftpd

   systemctl  enable  vsftpd



3. vi  /etc/vsftpd/vsftpd.conf

   19, 29,  33,  35

p674



4. chown  ftp.ftp  /var/ftp/pub

​    systemctl  restart   vsftpd



5.  window client program 설치

​    알드라이브 설치

​    192.168.111.101 

​    익명으로접속



-알드라이브 설치 후에

이클립스에 Dynamic Web Project 생성(파일명: linux) -> [index.html](http://index.html/) 생성 -> 'linux' Warfile
알드라이브 /pub 에 넣는다. /var/ftp/pub를 ls 하면 [linux.war](http://linux.war/) 가 있다.


stoptomcat
cp [linux.war](http://linux.war/) /usr/local/[apache-tomcat-9.0.37/webapps/](http://apache-tomcat-9.0.37/webapps/)
cd /usr/local/[apache-tomcat-9.0.37/webapps/](http://apache-tomcat-9.0.37/webapps/)
ls
mv ROOT ROOT_BACK
ls
mv [linux.war](http://linux.war/) [ROOT.war](http://root.war/)
ls
starttomcat

/usr/local/[apache-tomcat-9.0.37/webapps/](http://apache-tomcat-9.0.37/webapps/)에 자동으로 ROOT 를 생성