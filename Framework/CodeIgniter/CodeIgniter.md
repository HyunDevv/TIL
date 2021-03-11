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

