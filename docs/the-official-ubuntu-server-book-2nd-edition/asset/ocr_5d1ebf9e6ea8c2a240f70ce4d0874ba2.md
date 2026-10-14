# Nagios

Trending is an important part of any system monitoring, but collecting statistics is only one side of monitoring. The other side is getting alerts when a host or service goes down. There is a large number of great commercial and open source monitoring tools, but Nagios is the tool that seems to come up over and over. Nagios is an open source monitoring tool that has become popular among other reasons for its plug-in architecture. Not only is it relatively easy to write your own plug-ins to monitor specific things, but many of the common items you would want to monitor already have plug-ins written.

Nagios is a great tool, but if you talk to enough sysadmins who use it, you will find a common theme: It’s great but it can be a pain to configure. Nagios uses a series of different configuration files to configure hosts to monitor, services to check on those hosts, groups of hosts, and the rest of its settings. The syntax for any particular file isn’t too daunting in and of itself, but it does provide quite a learning curve for the uninitiated. If you have to monitor a large number of systems with Nagios, you end up doing one of two things: writing your own scripts to dump out Nagios configuration files, or using a Nagios front end for configuration. I tend to be on the side of not reinventing the wheel, so while I’ve written plenty of Nagios configuration files and scripts in my day, now I prefer the Web-based front ends.

Because of the power of Nagios a number of different individuals and companies have created monitoring software based on it. There are many excellent Nagios front ends to choose from, and choosing one to feature in this chapter is a tricky (and potentially controversial) task. In the end I settled on GroundWork Monitor Community Edition (http://groundworkopensource.com) for a few reasons:

+   It's an open source project.
+   Even though GroundWork is created and supported by a company that also has a commercial version of the product, the Community Edition is a completely open source project that is also free of charge.

+   Professional support is available.
+   Even though many Linux sysadmins are fine with not having commercial support for their software, often the people they work for aren’t. The GroundWork company doesn’t just offer support for its commer-