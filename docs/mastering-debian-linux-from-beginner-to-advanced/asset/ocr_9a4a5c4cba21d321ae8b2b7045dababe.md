2. Add the following configuration (adjust as needed):

```
```
server {
    listen 80;
    server_name mysite.com www.mysite.com;
    root /var/www/mysite;
    index index.html index.htm;

    location / {
        try_files $uri $uri/ =404;
    }
}
```
```

3. Create the document root directory:

```
```
sudo mkdir -p /var/www/mysite
```
```

4. Enable the virtual host by creating a symbolic link:

```
```
sudo ln -s /etc/nginx/sites-available/mysite
/etc/nginx/sites-enabled/
```
```

5. Test the Nginx configuration: