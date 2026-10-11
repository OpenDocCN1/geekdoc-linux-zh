FastCGI is a protocol to interface interactive programs with a web server – it’s an improvement over CGI (common gateway interface). CGI, while easy to implement, had problems in scaling since separate processes were created for each web request – a huge overhead for the host OS. FastCGI solves this by using persistent processes to serve series of web requests; moreover, these processes are owned by FastCGI server (flup in our case) and not the web server. This de-couples webs-server and FastCGI server, allowing effective scaling. Now any server that supports FastCGI can be used for MediaGoblin. Nginx is a good option because of easy configuration and setup.

# 08 Nginx setup

Nginx has been slowly rising in the ranks of the web server of choice and is currently one of the most used web servers. An acronym for Engine X, it is a high-performance HTTP server. It does support a lot of other protocols too but those are out of scope for us. Here. Let’s go straight to the server set up. Create a configuration file at /srv/mediagoblin.example.org/nginx.conf and create a symbolic link into a directory that will be included in your nginx configuration with one of the following commands (as the root user):

```
In -s /srv/mediagoblin.example.org/nginx.conf /etc/nginx/sites-enabled/
```

This way, a change in one file automatically reflects in the other. You need to then add the contents to the configuration file, as shown in the screenshot below. Remember to change the fields as per your local paths. Once done, restart nginx using sudo /etc/rc.d/nginx restart. If everything goes well, start MediaGoblin using:

```
cd /srv/mediagoblin.example.org/ mediagoblin/ ./lazyserver.sh --server-name=fcgi fcgi_host=127.0.0.1 fcgi_port=26543
```

Visit mediagoblin.com to see an example MediaGoblin gallery in action.

# 09 MediaGoblin home

The setup process is a little lengthy, and for the novice user it may seem a complex task, but the steps are simple and you just need to follow them one at a time. Once you have successfully completed the process, you can enjoy uninterrupted media streaming for you and your loved ones.

![](bbox=[0.39, 0.15, 0.9, 0.66])

The first step after you’re ready with your new MediaGoblin instance is to create an account. This is because you can browse the collections anonymously but you need an account to upload media. To create an account click on the ‘Log in’ button on the top-right corner. In the log in page that appears next, click on Create one here to open the user registration page. Fill the details in the registration page and you are good to go! Just log in with the credentials and then click on your user name to be redirected to your profile page. Here you have the options to upload media and manage your profile.

# 10 Add media

Adding a media file is a breeze, just click on the ‘Add media’ button on the right side of your profile page. In the next page, upload the file, set the title of the media, add a description, add tags and set the license you’d like to assign to the media. Finally click on the ‘Add’ button to upload the file. On the left-hand side of the page, you may notice that there is a ‘Browse Collections’ link. This option lets you browse through the collections that have been created by other users (if you are on a multi-user environment). A collection is a group of media files that are logically bundled together, generally with the intention of representing an event or other such scenarios. Note that media files can be added to these collections at any point in time and not just during the initial upload, so it’s worth checking them periodically. To top-right icon to reveal the account related options and then click on ‘Create new collection’. You can then add in the title and description to add your own collection.