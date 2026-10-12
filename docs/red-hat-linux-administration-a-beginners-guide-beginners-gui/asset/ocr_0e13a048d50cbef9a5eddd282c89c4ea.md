Apache provides a way to get around this using the `ServerName` directive. By specifying what you want Apache to return as the host name of the web server, a system with a name like dioxin can have an alias of www, invisible to users of the site. Here is an example of the `ServerName` directive:

```
```apache
ServerName www.eng.domain.org
```
```

# Server Administrator

It's often a good idea, for a couple of reasons, to use an e-mail alias for a web site's administrator. First, there may be more than one administrator. By using an alias, it's possible for the alias to expand out to a list of e-mail addresses. Second, if the current administrator leaves, you don't want to have to make the rounds of all those web pages and change the name of the site administrator.

Assuming you have set up the e-mail alias so that `www@domain.com` represents your web administrator(s) (see Module 13 for doing this in Linux), you need to edit the ServerAdmin line in the `httpd.conf` file so that it reads as follows:

```
```apache
ServerAdmin www@domain.com
```
```

# Prefork MPM

As I mentioned earlier, the Multi-Processing Module (MPM) is a new feature in Apache that allows closer integration with the native networking features of each operating system. The trick is that, unlike regular Apache modules, you can only select one MPM, and you have to do so when Apache is compiled. While some of the available MPMs are just not relevant to us on Linux (`mpm_winnt`, for example) there are still a few different features implemented at the MPM level. The hybrid process/threading model I mentioned earlier is one example. For compatibility reasons, the Apache package included with Red Hat has been compiled with the prefork MPM, as it follows the same process model that was used in the Apache 1.3 series. Unfortunately, if you want to use a different MPM, you'll have to recompile Apache. Even sticking with the prefork MPM, there are a number of settings that you can adjust for performance.

Using the prefork model, Apache will start a number of processes and have them wait around for incoming connections. Each process can handle a number of requests from the same client. When the load grows, more processes are forked to handle the additional connections. When the load dies down, extraneous idle processes are killed off. With this in mind, the following options should start to make more sense.

This is the number of processes that Apache will fork as a starting point when it first starts up:

```
```apache
StartServers        8
```
```

Apache will always keep at least this many processes around:

```
```apache
MinSpareServers     5
```
```