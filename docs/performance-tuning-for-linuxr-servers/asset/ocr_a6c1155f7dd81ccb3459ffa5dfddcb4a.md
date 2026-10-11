Additional enhancements that are part of the 2.5 and 2.6 kernels and that improved the performance of VolanoMark include the O(1) scheduler and the SMP scalable timer.

# SPECHTTPD

The SPECHTTPD benchmark presents a demanding workload to a web server. This workload requests 70% static pages and 30% simple dynamic pages. Sizes of the web pages range from 102 bytes to 921,000 bytes. The dynamic content models GIF advertisement rotation; there is no SSL content. SPECHTTPD is relevant because web serving, especially with Apache, is one of the most common uses of Linux servers. Apache is rich in functionality but is not designed for high performance. Apache was chosen as the web server for this benchmark because it currently hosts more web sites than any other web server on the Internet. SPECHTTPD is the accepted standard benchmark for web serving. SPECHTTPD stresses the following kernel components:

+   Scheduler

+   TCP/IP

+   Various threading models

+   SendFile

+   Zerocopy

+   Network drivers

Figures 21-6 and 21-7 show the results of SPECHTTPD using web static content and web dynamic content, respectively. Also included is a description of the hardware and software configurations used for each test.

![](bbox=[0.22, 0.71, 0.77, 0.75])