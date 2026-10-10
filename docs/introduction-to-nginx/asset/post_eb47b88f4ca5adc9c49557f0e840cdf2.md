
# INTRODUCTION TO NGINX

## TURBO BOOST YOUR WEB SERVER!

GABRIEL CÁNIPA

![](img/3adf2b91cc40e3d0012eab041f055ca8_0_0.png)

## Introduction to Nginx

## Contents

- 1 Nginx installation on Linux 1
  - 1.1 Introduction . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 1
  - 1.2 Installation of Nginx in Debian Wheezy 7.2 using online repositories . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 1
  - 1.3 Installation of Nginx in Debian Wheezy 7.2 from sources . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 3
  - 1.4 Installation of Nginx on Ubuntu 12.04 LTS . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 5
  - 1.5 Use of the checkinstall package to keep track of all the files created or modified by an installation script . . 8
  - 1.6 Installing Nginx in CentOS 6.4 . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 9
    - 1.6.1 From repositories . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 9
    - 1.6.2 From sources . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 10
    - 1.6.3 Enabling modules . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 10
  - 1.7 Adding Nginx as a system service . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 12
- 2 Nginx Configuration Guide 14
  - 2.1 Configuration file syntax . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 14
  - 2.2 Configuration directives . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 14
  - 2.3 Organization and inclusions . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 16
  - 2.4 Base modules . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 18
  - 2.5 The HTTP Server . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 20
  - 2.6 Mail server proxy . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 20
  - 2.7 Virtual hosts . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 21
- 3 Nginx and Apache 24
  - 3.1 Introduction . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 24
  - 3.2 Nginx as reverse proxy . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 24
  - 3.3 Nginx proxy module . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 25
  - 3.4 A note on variables . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 27
  - 3.5 Configuring Apache . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 27
  - 3.6 Configuring Nginx . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 30
  - 3.7 Separating content . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 31
  - 3.8 Download the configuration files . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 34
- 4 Load balancing with Nginx ... 35
  - 4.1 Introduction - The need for load balancing ... 35
  - 4.2 Necessary modules ... 35
    - 4.2.1 upstream module ... 35
  - 4.3 Download the configuration file ... 43
- 5 Nginx SSL configuration guide ... 44
  - 5.1 Introduction ... 44
  - 5.2 Adding support for SSL to Nginx ... 44
  - 5.3 Creating, signing, and using a certificate ... 45
  - 5.4 Download the files ... 55
- 6 Nginx Websockets proxying guide ... 56
  - 6.1 Introduction ... 56
  - 6.2 Installing Node.js ... 56
  - 6.3 Installing additional libraries ... 57
  - 6.4 So... what does Nginx has to do with all of this? ... 59
  - 6.5 Download source files ... 62

Copyright (c) Exelixis Media P.C., 2016

All rights reserved. Without limiting the rights under copyright reserved above, no part of this publication may be reproduced, stored or introduced into a retrieval system, or transmitted, in any form or by any means (electronic, mechanical, photocopying, recording or otherwise), without the prior written permission of the copyright owner.

## Preface

Nginx is an open source HTTP and reverse proxy server, as well as a mail proxy server, load balancer, and HTTP cache. The nginx project started with a strong focus on high concurrency, high performance and low memory usage. It runs on Linux, BSD variants, Mac OS X, Solaris, AIX, HP-UX, as well as on other *nix flavors. It also has a proof of concept port for Microsoft Windows. According to Netcraft nginx served or proxied 17.65% busiest sites in March 2014.

This ebook will introduce you to the magic of nginx. You will learn to install and configure nginx for a variety of software platforms and how to integrate it with Apache.

Additionally, you will get involved with more advanced concepts like Load Balancing, SSL configuration and Websockets proxying.

## About the Author

Gabriel's areas of expertise and interest are Linux system administration, shell scripting, database administration (SQL Server, MySQL, Oracle 11g), object-oriented and procedural programming (Python and PHP), desktop applications (C#, Visual Basic, Excel with VBA) and web development (jQuery, HTML5, CSS3, PHP).

He has also been working as a Level-1 TSR (Technical Support Representative) supporting onsite the startup and ongoing operation of the WMS in a major multinational company, running Red Hat Enterprise Linux and Oracle 11g as RDBMS.

# Chapter 1

## Nginx installation on Linux

### 1.1 Introduction

Nginx (pronounced “engine x”) is - in few words - a small, powerful, and scalable web/proxy server. According to a recent survey performed by Netcraft, Nginx powers more than 15% of the web, equating to 111,680,078 sites (Sept. 2013 Web Server Survey), including giants like Netflix and WordPress.com.

Nginx is available under the Simplified BSD License, an open source license, and can be installed either from online repositories or from sources. In this article we will cover the installation of Nginx in Debian, Ubuntu, and CentOS using both methods. It is important to note that the repositories are often somewhat out-of-date. If we want the latest features and bugfixes, it’s recommended to build from source or use packages directly from nginx.org.

### 1.2 Installation of Nginx in Debian Wheezy 7.2 using online repositories

Using aptitude, the high-level interface to the Debian GNU/Linux package manager, we can check the list of packages related to Nginx (see Fig. 1.1). However, it is advisable to run the command aptitude update first in order to see an updated list of available packages.

```
root@debian:~# aptitude search nginx
p    nginx-common                   - small, powerful, scalable web/proxy server - common files
p    nginx-doc                      - small, powerful, scalable web/proxy server - documentation
p    nginx-extras                   - nginx web/proxy server (extended version)
p    nginx-extras-dbg               - nginx web/proxy server (extended version) - debugging symbols
p    nginx-full                     - nginx web/proxy server (standard version)
p    nginx-full-dbg                 - nginx web/proxy server (standard version) - debugging symbols
p    nginx-light                    - nginx web/proxy server (basic version)
p    nginx-light-dbg                - nginx web/proxy server (basic version) - debugging symbols
p    nginx-naxsi                    - nginx web/proxy server (version with naxsi)
p    nginx-naxsi-dbg                - nginx web/proxy server (version with naxsi) - debugging symbols
p    nginx-naxsi-ui                 - nginx web/proxy server - naxsi configuration front-end
root@debian:~#
```

![](img/3adf2b91cc40e3d0012eab041f055ca8_7_0.png)

(By the way, the letter “p” in the first column indicates that no trace of the package currently exists on the system).

If we can’t decide which package to install, aptitude search followed by a package name such as aptitude search nginx- is our friend and will help us to make up our minds as to which one is right for us. Based on the description of each package listed above, we will proceed with the installation of nginx-full (see Fig. 1.2). It is important to note that the
