# Network Utilities

Whether your computer is on a local network or using the Internet, there are several network commands that you may find quite useful. There are several basic network-oriented commands you probably need to be familiar with. Each of these can provide very useful information about your connection to a network or the Internet, as well as help diagnose specific connectivity problems.

# ifconfig

This is the first network command we will examine. The Windows equivalent is `ipconfig`, and it provides virtually identical information to `ifconfig`. The `ifconfig` command just gives a little extra data. Basically, the information it supplies regards the status of your network card and your connection to the Internet. The output of this command is shown in Figure 18.11.

![](bbox=[0.04, 0.3, 0.65, 0.61])

The `ifconfig` command will tell you if your network card is up and running. If you are currently connected to a local network or the Internet, it will send out packets periodically to ensure that you still are connected. This command also will display the IP address of your computer’s network card. `ifconfig` is discussed in more detail in Chapter 19, “Linux Administration from the Shell.”

# ping

The `ping` utility is much like a SONAR ping on a submarine. It sends out packets to a given IP address, as shown in Figure 18.12, and tells you whether or not they were received. One of the first things to check if you are having trouble getting on a network or the Internet is to try and ping a known IP address. You also can ping Internet sites by their names. For example, you can try to ping www.chuckeaston.com. If you find that you cannot get a response from any site you ping, then you are probably not connected to the Internet. If you can get some sites to respond and not others, then the problem most likely lies with those sites. The `ping` command works exactly the same from a Windows command prompt as it does in a Linux or Unix shell.