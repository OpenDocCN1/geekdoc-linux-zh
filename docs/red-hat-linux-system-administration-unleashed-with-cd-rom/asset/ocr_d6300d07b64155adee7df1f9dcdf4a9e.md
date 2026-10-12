# Introduction to Web Serving

The past few years have seen the incredible growth of the Internet. Just a decade ago, the Internet was used by only a specialized group of individuals; today it is a household name and is having a significant impact upon society as a whole. With the growth of the Internet has the come the obvious growth of Web servers. There are now a large number of Web servers available, both commercial and free.

While the Linux operating system has much merit and is the platform of choice for many computing solutions, more and more people are turning to Linux as a Web server platform. Red Hat Linux is a ready to run Web server out-of-the-box, and obviously much more. In this chapter, we will be looking at using Red Hat Linux as a Web server; in particular we will be examining the Apache Web server in detail. Apache is the default Web server that comes with Red Hat Linux 6.1. We will also be taking a quick look at other Web servers that are available for Linux, including Boa, dhttpd, fhttpd, ghttpd, Roxen, thttpd, and WN.

# Apache

The default Web server that ships with Red Hat Linux 6.1, and many other Linux distributions for that matter, is Apache. Apache is currently the most popular Web server on the internet today, and runs on many different architectures besides Linux; including Solaris, HPUX, SVR4, SunOS 4.x, A/UX, the BSD family, and even Windows NT. Linux is definitely one of the more popular platforms for running Apache on due to its low cost and stability.

The Apache Project, like Linux, is another free software success story; the goal of which is to create a full-featured, robust, commercial-grade Web server. Over the years, there have been many people who have contributed code, ideas, and money to the Apache project, and have helped Apache become the success that it is. There is a core group of volunteers from all around the world known as the Apache Group; they help with the coordination and continual development of Apache. In this section, we will look in detail at how Apache came to be, how to get started using Apache, and how to tweak and configure it so that it does what you want it to.

# About the Apache Project

Just a few years ago, the most popular HTTP server of the time was the NCSA httpd. In mid-1994, the main developer for the NCSA httpd left the project, leaving many Webmasters around the world to tinker with the code for httpd. Eventually, there were a number of enhancements and bug fixes that were developed for httpd; these changes where distributed in the form of source code patches. It wasn't long until the number of patches