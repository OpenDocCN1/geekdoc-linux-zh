Apache’s features are provided by modules for several reasons:

+   - Loading unneeded features wastes resources, particularly memory.
+   - If you don’t load a feature, bugs in it can never cause you problems.
+   - Breaking features into modules generally leads to better design.
+   - Modules can be written by groups other than Apache and then integrated by the user.

Before Apache 1.3, modules had to be chosen at compile time. They were then statically linked into Apache so that they were always available. With version 1.3, Apache added the Dynamic Shared Object (DSO) model, which allows modules to be installed at run time with LoadModule directives in the httpd.conf file.

To use DSO modules, you must install the mod_so module statically (that is, at compile time), but after that, most modules can be installed at runtime. There are some tradeoffs, however. In particular, startup will be approximately 20% slower and execution will be approximately 5% slower. For heavily loaded sites, this is generally unacceptable, but for smaller sites that can afford the overhead, you can gain the flexibility of adding and removing modules simply by updating your httpd.conf file and restarting Apache (instead of recompiling and reinstalling Apache). For more information on DSO modules, see http://www.apache.org/docs/dso.html.

# USING APACHE WITH SSL

Earlier in this chapter, authorization and access control were discussed as two important aspects of your Web site security. This section deals with another aspect of security: making the communications between the clients and your Web server private. This is done by encrypting the communications between the clients and the server, using the Secure Sockets Layer (SSL) protocol.

This section gives an overview of the mechanisms that are used for secure communications, as well as providing some information about the mod_ssl modification to Apache, which allows it to function as a secure Web server. This section also discusses some of the creation and manipulation of special data files that are used for secure communications.

The availability of SSL for use with your Web server creates some interesting dilemmas for governments that want to control encryption to avoid having it fall into the hands of foreign entities that they want to spy on. This topic is discussed as well.

# OVERVIEW OF SECURE COMMUNICATIONS CONCEPTS

SSL is a protocol that was originally defined by Netscape Communications Corporation to allow two machines communicating over TCP/IP to encrypt the information sent between them. After a communication session is secured in this way, the two machines can exchange private or sensitive information without worrying about eavesdroppers or other interlopers stealing or using the information. This is an essential feature for Web servers used for