# FIGURE 18.2
Running the test-cgi CGI on Apache.

![](bbox=[0.33, 0.12, 0.89, 0.66])

# Allowing Users to Have Personal Web Pages

So far, any Web pages you want to add to the server Web site must be placed in the DocumentRoot, which is /usr/local/httpd/htdocs/ in SuSE Linux. If your users want to have their own Web pages, they must ask you to post them. You can do this by creating a subdirectory for every user under /usr/local/httpd/htdocs and placing their Web content in it. This is very time-consuming, especially if you have many users and they update their Web pages frequently.

Apache solves this problem by allowing your users to put Web pages in their home directories. This enables them to control the content and update it without your help, removing quite a load off the system administrator. The SuSE team has already configured Apache for this, so all you need to do is uncomment a few lines in /etc/httpd/httpd.conf. The lines are as follows:

```
UserDir public_html
<Directory /home/*/public_html>
    AllowOverride FileInfo AuthConfig Limit
    Options MultiViews Indexes SymLinksIfOwnerMatch IncludesNoExec
    <Limit GET POST OPTIONS PROPFIND>
        Order allow,deny
        Allow from all
```