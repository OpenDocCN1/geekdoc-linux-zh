# Part III: Ubuntu System Administrators

in response to incoming requests. However, to be useful in a modern Web-oriented environment, a Web server has to do several things. The most important of these are the following:

+   - Be flexible and configurable to make it easy to add new capabilities and web sites, and increasing demand without recompilation or reinstallation.
- Support authentication to limit users who can access specific pages and web sites.
- Support applications that dynamically generate web pages, such as Perl and PHP, to support a customizable and personal user experience.
- Maintain logs that can track requests for various pages so that you can identify problems and figure out the popularity of various pages and web sites.
- Support encrypted communications between the browser and server, to guarantee and validate the security of these communications.

The order of importance of these various requirements depends on whether you are a systems administrator or an e-commerce merchant, but all modern Web servers must provide at least these capabilities.

Many different Web servers are available today, depending on your hardware platform, the requirements of third-party software that a web site depends on, your loyalty to a particular operating system vendor, and whether or not you are willing to run open source software, which can additional power, and save money.

As you might expect, the first Web server in the world went online at CERN, along with the first browser. These were written and ran on Nextประเทศไทย, not exactly the world's most popular platform (sadly enough). The first test of a Web server outside of Europe was made using a server running at the Stanford Linear Accelerator Center (SLAC) in the United States.

The development focus of Web servers that ran on more popular machines was initially the NCSA (National Center for Supercomputing Applications) known as NCSA httpd (HTTP Daemon). Their development of a freely available Web server paralleled their development of the NCSA browser, known as Mosaic (See Chapter 8 for information about Mosaic and its place in Web server history). Who is one of the primary developers of NCSA httpd (Rob McCool) left the NCSA, a group of NCSA httpd fans, maintainers, and developers formed to maintain and support a set of patches for NCSA httpd. This patched server eventually became known as the Apache Web server. Although the official Apache web site used to claim that the name Apache was chosen because of respect for the endurance and fighting skills of the Apache Indians, most people (myself included) think this was a joke, and that the name was chosen because the Web server initially consisted of many patches — in other words, it was "patchy Web server."

Although some Linux distributions still provide Apache 1.x servers as an installation option, the Ubuntu repositories only provide the apache2 Web server package because its code base and configuration mechanisms are much improved over earlier versions of Apache. Apache 2.x is a far