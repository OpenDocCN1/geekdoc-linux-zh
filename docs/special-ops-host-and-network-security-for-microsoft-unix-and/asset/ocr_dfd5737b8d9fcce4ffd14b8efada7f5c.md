# Hacking Custom Web Applications • Chapter 11

WebProxy contains far than just HTTP rewriting, and is bundled with additional plug-ins to do “fuzzing” and even some encoding, decoding, and hashing functions. The end result of our cookie example, with a few points and a few clicks, is shown in Figure 11.19.

# Figure 11.19 Logged in as User j-j

![](bbox=[0.247, 0.213, 0.752, 0.488])

# State Tracking

Many of the problems with authentication and authorization stem from applications' failure to effectively keep state. This problem is a well-known one and several solutions to address it. Many of the implementations of these solutions, however, are flawed and can be bypassed by a little bit of effort.

# The Developers Challenge

When developing custom Applications, a big problem that developers face is the uncertainty of exactly who is sitting at the client end of the application. This problem is resolved by means of strong authentication and the use of SSLv3 client-side certificates.

Another problem that presents itself is of keeping state. HTTP requests that are sent to a Web server are distinct TCP connections. A user browsing a single Web page might make several TCP connections to different servers. The question there is whether subsequent pages within an application keep state of the current environment. For example: A user logs in to a Web application for Internet banking, makes some changes to her personal settings, then checks her balances on three of her accounts.