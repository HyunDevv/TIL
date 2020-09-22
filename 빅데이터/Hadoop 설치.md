#  Hadoop 설치

1.  리눅스 서버를 준비한다

   	+ hostname  설정

2. 자바를 설치한다

3. 하둡 설치

   > 네트워크 상의 다른 컴퓨터에 로그인하거나 원격 시스템에서 명령을 실행하고, 다른 시스템으로 파일을 복사할 수 있게 해주는 응용 프로토콜. 암호화 기법을 사용한다

   0.  Firewall stop

      \- systemctl stop firewalld

      \- systemctl disable firewalld

   1. 보안 설정 (public, pirvate key를 생성)(가상분산모드)

      ssh-keygen -t dsa -P '' -f ~/.ssh/id_dsa

      cd

      cd .ssh

      cat id_dsa.pub >> authorized_keys

      [root@server .ssh]# ls
      authorized_keys  id_dsa  id_dsa.pub

      - dsa는 암호화 방식
      - 자기컴으로 들어갈 때도 필요

      ssh hadoopserver (확인 후 exit)

   2. hadoop 설치

      wget https://archive.apache.org/dist/hadoop/common/hadoop-1.2.1/hadoop-1.2.1.tar.gz

      tar xvf hadoop-1.2.1.tar.gz 

      cp -r hadoop-1.2.1 /usr/local

      vi /etc/profile

      HADOOP_HOME 지정 (52줄)

      ```bash
      JAVA_HOME=/usr/local/jdk1.8.0
      CLASSPATH=/usr/local/jdk1.8.0/lib
      HADOOP_HOME=/usr/local/hadoop1.2.1
      export JAVA_HOME  CLASSPATH HADOOP_HOME
      PATH=$JAVA_HOME/bin:$HADOOP_HOME/bin:.:$PATH
      ```

      

   3. 환경설정 파일 수정

      

      cd /usr/local/hadoop-1.2.1/conf에서!!

      

      vi core-site.xml

      <configuration>

      <property>

      <name>fs.default.name</name>

      <value>hdfs://localhost:9000</value>

      </property>

      <property>

      <name>hadoop.tmp.dir</name>

      <value>/usr/local/hadoop-1.2.1/tmp</value>

      </property>

      </configuration>

      

      vi hdfs-site.xml

      <configuration>

      <property>

      <name>dfs.replication</name>

      <value>1</value> 

      </property>

      <property>

      <name>dfs.webhdfs.enabled</name>

      <value>true</value>

      </property>

      <property>

      <name>dfs.name.dir</name>

      <value>/usr/local/hadoop-1.2.1/name</value>

      </property>

      <property>

      <name>dfs.data.dir</name>

      <value>/usr/local/hadoop-1.2.1/data</value>

      </property>

      </configuration>

      

      vi mapred-site.xml

      <configuration>

      <property>

      <name>mapred.job.tracker</name>

      <value>localhost:9001</value>

      </property>

      </configuration>

      

      vi hadoop-env.sh

      9 export JAVA_HOME=/usr/local/jdk1.8.0

      10 export HADOOP_HOME_WARN_SUPPRESS="TRUE"

      

   4. Hadoop 실행
      ssh hadoopserver

      hadoop namenode -format 하면 name 폴더가 만들어진다

      start-all.sh

      jps

      

      firefox에서 http://hadoopserver:50070 로 확인

      

- 초기화 하려면?

  0. stop-all.sh

  1. /usr/local/hadoop-1.2.1/name, data, tmp 삭제
  2. .ssh에 있는 키값 삭제

---

- 리눅스 끌 때

  stop-all.sh 하고 끈다