# 리눅스에 MariaDB 설치하기/삭제하기

## 설치하기

1. download

   https://downloads.mariadb.com/MariaDB/mariadb-10.0.15/yum/centos7-amd64/rpms/

   \- client, common, server



​	yum -y remove mariadb-libs

​	yum -y localinstall Maria*



​	systemctl restart mysql

​	systemctl status mysql

​	chkconfig mysql on



​	mysqladmin -u root password '111111'



​	mysql -h localhost  -u  root  -p



​	use mysql;



​	SELECT  user, host  FROM  user;



​	GRANT   ALL   ON   *.*  TO   user1@'192.168.111.%'  IDENTIFIED  BY  '111111';



​	CREATE   DATABASE   shopdb   CHARACTER   SET   utf8;



​	use   shoppdb



## 삭제하기

​	systemctl   stop  mysql



​	yum -y  remove Maria*

 

​	mariadb 관련 폴더들을 삭제한다.

 

​	rm -rf /etc/my.cnf*

​	rm -rf /var/log/mysql  

​	rm -rf /var/lib/mysql 