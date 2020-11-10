# Tomcat 설치

tomcat.apache.org

tar xvf apachxxx.gz

cp -r apache-tomcat-xx /usr/local

cd /usr/local/apache-tomcat-xx

cd conf

vi server.xml - 69번쨰줄 8080 -> 80 port

cd /usr/bin

ln -s /usr/local/apache-tomcat-9.0.37/bin/startup.sh starttomcat

ln -s /usr/local/apache-tomcat-9.0.37/bin/shutdown.sh stoptomcat



## 리눅스에서 자바프로젝트 실행

cd /usr/local/[apache-tomcat-9.0.37/webapps/](http://apache-tomcat-9.0.37/webapps/)
ls
mv ROOT ROOT_BACK
ls
mv [linux.war](http://linux.war/) [ROOT.war](http://root.war/)
ls
starttomcat

/usr/local/[apache-tomcat-9.0.37/webapps/](http://apache-tomcat-9.0.37/webapps/)에 자동으로 ROOT 를 생성



포트확인 : netstat -tlnp