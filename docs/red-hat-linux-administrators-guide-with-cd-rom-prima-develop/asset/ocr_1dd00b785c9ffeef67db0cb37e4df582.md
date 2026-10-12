communicates with other machines. This chapter deals with some of the more basic networking configuration issues such as routing, IP addressing, and domain names. It will not go into great depth for more complex networking and routing issues but instead will look at how Linux handles networked topics and how you can optimize Linux to work on networked systems.

# ## Understanding Networking Basics

The most basic functions associated with networking use the ISO/OSI model (see Table 15.1). This outline was originally designed to explain the relationship of hardware to software to data and has been adopted by nearly all facets of networking paradigms to explain the varying depths of networking currently available today. To understand how networking works, you must first look at how it is configured to operate. The ISO/OSI model specifies the manner in which information passes from the lowest level, that of hardware or physical structures, to the higher level, that of software, which in turn makes the information accessible to users for processing.

# **Table 15.1 The OSI Model in Simple Terms**

| Layer | Name | Purpose |
|---|---|---|
| 1 | Physical layer | Provides the cable or physical connection for transmitting information |
| 2 | Data link layer | Sends and receives packets, and identifies hardware addresses |
| 3 | Network layer | Sets up the routing and keeps track of transmissions |
| 4 | Transport layer | Verifies the correct reception of data on both ends |
| 5 | Session layer | Authenticates and authorizes packets transmissions |
| 6 | Presentation layer | Handles data errors and compression |
| 7 | Application layer | Provides user services, such as mail, Telnet, and FTP |


Though the ISO/OSI model is used primarily for network design, the world of networking often refers to the model. Having a basic grasp of its structure and purpose is essential to understanding how the Internet and networking between machines operate.

For most Linux administrators, most networking configurations will be a simple matter of installing an Ethernet card into an internal slot within your Linux box,