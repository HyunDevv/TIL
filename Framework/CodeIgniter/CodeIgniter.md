# CodeIgniter

index.php 제거하기 : **https://bogyum-uncle.tistory.com/83**

database 연결 : https://opentutorials.org/course/697/3827#databasephp

- Topic.php

```php
<?php if ( ! defined('BASEPATH')) exit('No direct script access allowed');
class Topic extends CI_Controller {
    function index(){
        $this->load->view('Topic');
    }
    function get($idd){
        $data = ['id'=>$idd];
        $this->load->view('Get',$data);
    }
}
?>
```



- Get.php

```php
<!DOCTYPE html>
<html>

<head>
    <meta charset="utf-8" />
</head>

<body>
    토픽 <?=$id?>
</body>

</html>
```





## session

```shell
MariaDB [opentutorials]> CREATE TABLE IF NOT EXISTS `ci_sessions` (
    -> `id` varchar(128) NOT NULL,
    -> `ip_address` varchar(45) NOT NULL,
    -> `timestamp` int(10) unsigned DEFAULT 0 NOT NULL,
    -> `data` blob NOT NULL,
    -> KEY `ci_sessions_timestamp` (`timestamp`)
    -> );
Query OK, 0 rows affected (0.012 sec)

MariaDB [opentutorials]> desc ci_sessions;
+------------+------------------+------+-----+---------+-------+
| Field      | Type             | Null | Key | Default | Extra |
+------------+------------------+------+-----+---------+-------+
| id         | varchar(128)     | NO   |     | NULL    |       |
| ip_address | varchar(45)      | NO   |     | NULL    |       |
| timestamp  | int(10) unsigned | NO   | MUL | 0       |       |
| data       | blob             | NO   |     | NULL    |       |
+------------+------------------+------+-----+---------+-------+
4 rows in set (0.024 sec)

MariaDB [opentutorials]> select * from ci_sessions;
+----------------------------+------------+------------+--------------------------------------------------------------+
| id                         | ip_address | timestamp  | data                                                         |
+----------------------------+------------+------------+--------------------------------------------------------------+
| vi5nfhu4vhakec2o7qu0pvl8j3 | 127.0.0.1  | 1615871313 | __ci_last_regenerate|i:1615871312;session_test|s:6:"egoing"; |
| vlcl5ughtckuvairatsf9uuidk | 127.0.0.1  | 1615871388 | __ci_last_regenerate|i:1615871387;session_test|s:6:"egoing"; |
| a8v34ebr8jbquoh1pl2v1juojr | 127.0.0.1  | 1615871433 | __ci_last_regenerate|i:1615871432;session_test|s:6:"egoing"; |
| 7jj8ldhdgmqcdoh6478q65kaqg | 127.0.0.1  | 1615871471 | __ci_last_regenerate|i:1615871471;session_test|s:6:"egoing"; |
+----------------------------+------------+------------+--------------------------------------------------------------+
4 rows in set (0.000 sec)
```

