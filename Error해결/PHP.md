# PHP

![image-20210312121556752](C:%5CUsers%5Ckjhkj%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20210312121556752.png)

- nginx/conf/nginx.conf에  fastcgi_param을 잘 확인한다

        location ~ \.php$ {
            root           html;
            fastcgi_pass   127.0.0.1:9000;
            fastcgi_index  index.php;
            fastcgi_param  SCRIPT_FILENAME  $document_root$fastcgi_script_name;
            include        fastcgi_params;
        }
