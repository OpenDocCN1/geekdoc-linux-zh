
![](img/2045828cf45e5632bf056f9ca99d6755_730_0.png)

FIGURE 26.1 Setting up Firefox to use 127.0.0.1 routes all its web requests through Squid.

## Access Control Lists

The main Squid configuration file is /etc/squid/squid.conf, and the default Fedora configuration file is full of comments to help guide you. The default configuration file allows full access to the local machine but denies the rest of your network. This is a secure place to start; we recommend you try all the rules on yourself (localhost) before rolling them out to other machines.

Before you start, open two terminal windows as root. In the first, change to the directory /var/log/squid and run this command:

```
tail -f access.log cache.log
```

That command reads the last few lines from both files and (thanks to the -f flag) follows them so that any changes appear in there. This allows you to watch what Squid is doing as people access it. We will refer to this window as the *log window*, so keep it open. In the other window (as root, remember), bring up the file /etc/squid/squid.conf in your favorite editor. This window will be referred to as the *config editor*, and you should keep it open also.

To get started, search for the string `acl all`—this brings you to the access control section, which is where most of the work needs to be done. There is a lot you can configure elsewhere, but unless you have unusual requirements, you can leave the defaults in place.

> **NOTE**
> The default port for Squid is **3128**, but you can change that by editing the `http_port` line. Alternatively, you can have Squid listen on multiple ports by having multiple `http_port` lines: **80**, **8000**, and **8080** are all popular ports for proxy servers.

The `acl` lines make up your access control lists. The first 16 or so lines define the minimum recommended configuration for setting up which ports to listen to, and so on. You can safely ignore them. If you scroll down farther (past another short block of comments), you come to the `http_access` lines, which are combined with the `acl` lines to dictate who can do what. You can (and should) mix and match `acl` and `http_access` lines to keep your configuration file easy to read.

Just below the first block of `http_access` lines is a comment like `# INSERT YOUR OWN RULE(S) HERE TO ALLOW ACCESS FROM YOUR CLIENTS`. This is just what we are going to do. First, though, scroll just a few lines further and you should see these two lines:

```
http_access allow localhost
http_access deny all
```

They are self-explanatory: The first says, "allow HTTP access to the local computer, but deny everyone else." This is the default rule, as mentioned earlier. Leave that in place for now, and run `service squid start` to start the server with the default settings. If you have not yet configured the local web browser to use your Squid server, do so now so you can test the default rules.

In your web browser (Firefox is assumed from here on, but it makes little difference), go to the URL `http://fedora.redhat.com`. You should see it appear as normal in the browser, but in the log window you should see a lot of messages scroll by as Squid downloads the site for you and stores it in its cache. This is all allowed because the default configuration allows access to the localhost.

Go back to the config editor window and add the following before the last two `http_access` lines:

```
http_access deny localhost
```

So, the last three lines should look like this:

```
http_access deny localhost
http_access allow localhost
http_access deny all
```

Save the file and quit your editor. Then, run this command:

```
kill -SIGHUP `cat /var/run/squid.pid`
```

That command looks for the PID of the Squid daemon and then sends the `SIGHUP` signal to it, which forces it to reread its configuration file while running. You should see a string of messages in the log window as Squid rereads its configuration files. If you now go back to Firefox and enter a new URL, you should see the Squid error page informing you that you do not have access to the requested site.

The reason you are now blocked from the proxy is because Squid reads its ACL lines in sequence, from top to bottom. If it finds a line that conclusively allows or denies a request, it stops reading and takes the appropriate action. So, in the previous lines, localhost is being denied in the first line and allowed in the second. When Squid sees localhost asking for a site, it reads the deny line first and immediately sends the error page—it does not even get to the allow line. Having a `deny all` line at the bottom is highly recommended so that only those who explicitly allow are able to use the proxy.

Go back to editing the configuration file and remove the `deny localhost` and `allow localhost` lines. This leaves only `deny all`, which blocks everyone (including the localhost) from accessing the proxy. Now we are going to add some conditional allow statements: We want to allow localhost only if it fits certain criteria.

Defining access criteria is done with the `acl` lines, so above the `deny all` line, add this:

```
acl newsites dstdomain news.bbc.co.uk slashdot.org
http_access allow newsites
```

The first line defines an access category called newsites, which contains a list of domains (dstdomain). The domains are news.bbc.co.uk and slashdot.org, so the full line reads, "create a new access category called newsites, which should filter on domain, and contain the two domains listed." It does not say whether access should be granted or denied to that category; that comes in the next line. The line `http_access allow newsites` means, "allow access to the category newsites with no further restrictions." It is not limited to localhost, which means this applies to every computer connecting to the proxy server.

Save the configuration file and rerun the `kill -SIGHUP` line from before to restart Squid; then go back to Firefox and try loading `http://fedora.redhat.com`. You should see the same error as before because that was not in our newsites category. Now try `http://news.bbc.co.uk`, and it should work. However, if you try `http://www.slashdot.org`, it will not work, and you might also have noticed that the images did not appear on the BBC News website either. The problem here is that specifying `slashdot.org` as the website is very specific: It means that `http://slashdot.org` will work, whereas `http://www.slashdot.org` will not. The BBC News site stores its images on the site `http://newsimg.bbc.co.uk`, which is why they do not appear.

Go back to the configuration file, and edit the newsites ACL to this:

```
acl newsites dstdomain .bbc.co.uk .slashdot.org
```

Putting the period in front of the domains (and in the BBC's case, taking the `news` off also) means that Squid will allow any subdomain of the site to work, which is usually what you will want. If you want even more vagueness, you can just specify `.com` to match `*.com` addresses.

Moving on, you can also use time conditions for sites. For example, if you want to allow access to the news sites in the evening, you can set up a time category using this line:

```
acl freetime time MTWFFAS 18:00-23:59
```

This time, the category is called `freetime` and the condition is `time`, which means we need to specify what time the category should contain. The seven characters following that are the days of the week: Monday, Tuesday, Wednesday, Thursday, Friday, Saturday, and Sunday. Thursday and Saturday use capital T and S so that they do not clash with Tuesday and Sunday.

With the `freetime` category defined, you can change the `http_access` line to include it, like this:

```
http_access allow newsites freetime
```

For Squid to allow access now, it must match both conditions—the request must be for either `*.bbc.co.uk` or `*.slashdot.org`, and during the time specified. If either condition does not match, the line is not matched and Squid continues looking for other matching rules beneath it. The times you specify here are inclusive on both sides, which means users in the `freetime` category will be able to surf from 18:00:00 until 23:59:59.

You can add as many rules as you like, although you should be careful to try to order them so that they make sense. Keep in mind that all conditions in a line must be matched for the line to be matched. Here is a more complex example:

- You want a category `newsites` that contains serious websites people need for their work.
- You want a category `playsites` that contains websites people do not need for their work.
- You want a category `worktime` that stretches from 09:00 to 18:00.
- You want a category `freetime` that stretches from 18:00 to 20:00, when the office closes.
- You want people to be able to access the news sites, but not the play sites, during working hours.
- You want people to be able to access both the news sites and the play sites during the free time hours.

To do that, you need the following rules:

```
acl newsites dstdomain .bbc.co.uk .slashdot.org
acl playsites dstdomain .tomshardware.com fedora.redhat.com
acl worktime time MTWHF 9:00-18:00
acl freetime time MTWHF 18:00-20:00
http_access allow newsites worktime
```
