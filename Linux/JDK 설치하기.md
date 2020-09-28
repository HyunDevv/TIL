# 리눅스에 JDK 설치하기

1. 오라클에서 자바 다운(Linux x64 Compressed Archive) (jdk-8u261-linux-x64.tar.gz)
2. tar xvf jdk-8u261-linux-x64.tar.gz
3. mv jdk1.8.0_261 jdk1.8.0
4. cp -r jdk1.8.0 /usr/local
5. vi /etc/profile 53라인에 
   JAVA_HOME=/usr/local/jdk1.8.0
   CLASSPATH=/usr/local/jdk1.8.0/lib
   PATH=$JAVA_HOME/bin:.:$PATH
6. cd /usr/bin
   rm java
   ln -s /usr/local/jdk1.8.0/bin/java java
   java -version (확인)