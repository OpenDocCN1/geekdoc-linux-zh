# Chapter 4 · Using Common Linux Programs

Instead, mobile computing typically focuses on small programs known as apps. In the case of Android, you can download apps by using an app called Google Play. (A web-based version is available at https://play.google.com/store.) Apps typically provide quick and specialized computation, often employing features of the phone. For instance, an app can calculate the calories that you've burned while riding a bicycle or retrieve a weather forecast for your area. Both of these examples use your phone's GPS features to identify the phone's (and you) position.

Although most Linux applications for desktop and server computers are open source and available free of charge, some Android apps are not free. Be sure to check the cost before you download an app.

Android apps are increasingly a source of malware. You can minimize your risk by downloading apps from Google Play or other trustworthy stores.

# Using Server Programs

Linux is a powerful OS for server programs, so it should come as no surprise that you can find a variety of server programs for Linux. In the following pages, some server protocols and the programs that use them are described. In addition, the process of installing and launching servers is covered, as well as basic information on server security issues.

# Identifying Common Server Protocols and Programs

Networks, including the Internet, function by means of network protocols. Network protocols are clearly defined descriptions of how two computers should exchange data to achieve a particular end, such as transferring email or delivering a file to be printed. Most protocols are described in one or more standards documents, known as Request for Comments (RFC) documents, each of which has a number. Typically, one RFC document defines the protocol, and over time additional RFC documents define extensions or protocol modifications as they become necessary.

Most network protocols involve transferring data over one or more ports, which are numbered resources on a computer. You can think of a port as something like a telephone extension number—the main number (an Internet Protocol, or IP, address) identifies the computer as a whole, and the port number identifies the protocol being used. A server program attaches itself to a port number and receives all incoming requests on that port.

Table 4.1 summarizes some port numbers, the protocols with which they're associated, and the Linux programs that are often used in conjunction