# Tomcat 설치

tomcat.apache.org

tar xvf apachxxx.gz

cp -r apache-tomcat-xx /usr/local

cd /usr/local/apache-tomcat-xx

cd conf

vi server.xml - 69 -> 80 port

cd /usr/bin

ln -s /usr/local/apache-tomcat-9.0.37/bin/startup.sh starttomcat

ln -s /usr/local/apache-tomcat-9.0.37/bin/shutdown.sh stoptomcat