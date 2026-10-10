```
```
server {
    listen    80;
    server_name localhost;
    root /home/gacanepa/nginx-1.5.6/html;
    access_log /home/gacanepa/nginx-1.5.6/html/access_log;
    location / {
        index index.html index.htm;
    }
    location /restricted {
        index index.html index.htm;
        access_log off;
    }
}
```
```

Figure 2.2: Nested directive blocks

```
```
gacanepa@ubuntuOS:~/ngl15.5.6/html$ ls -l
total 20
-rw-r--r-- 1 gacanepa gacanepa 537 Oct 1 10:44 50x.html
-rw-r--r-- 1 root root 157 Oct 31 15:41 access_log
-rw-rw-r-- 1 gacanepa gacanepa 9 Oct 30 12:23 add.html
-rw-rw-r-- 1 gacanepa gacanepa 612 Oct 1 10:44 index.html
-rw-r--r-- 1 root root 306 Oct 31 15:50 main_access_log
gacanepa@ubuntuOS:~/ngl15.5.6/html$ cat access_log
127.0.0.1 - [31/Oct/2013:15:41:59 -0300] "GET /50x.html HTTP/1.1" 404 168 "-" "Mozilla/5.0 (X11; Ubuntu; Linux 1686; rv:23.0) Gecko/20100101 Firefox/23.0"
gacanepa@ubuntuOS:~/ngl15.5.6/html$ cat main_access_log
127.0.0.1 - [31/Oct/2013:15:49:31 -0300] "GET / HTTP/1.1" 304 0 "-" "Mozilla/5.0 (X11; Ubuntu; Linux 1686; rv:23.0) Gecko/20100101 Firefox/23.0"
127.0.0.1 - [31/Oct/2013:15:50:13 -0300] "GET /index.html HTTP/1.1" 200 612 "-" "Mozilla/5.0 (X11; Ubuntu; Linux 1686; rv:23.0) Gecko/20100101 Firefox/23.0"
gacanepa@ubuntuOS:~/ngl15.5.6/html$
```
```

Figure 2.3: Access logs

# 2.3 Organization and inclusions

Let's focus on line 17. There is a special directive there: include. This directive is used to insert the contents of the specified file at this exact location. The name of the file can be specified either by an absolute path or a relative path to the current directory (as it is in this case). We can see that there's a file named mime.types in the same directory as nginx.conf (see Fig. 2.4).