# ## Chapter 6

# # Nginx Websockets proxying guide

# ## 6.1 Introduction

According to the RFC (Request For Comments) #64551, issued by the IETF (Internet Engineering Task Force), WebSocket is a protocol providing full-duplex communications channels over a single TCP connection and is designed to be implemented in web browsers and servers, but it can be used by any client or server application.

Like TCP, WebSocket makes full-duplex communication possible in a low latency connection, but it differs from TCP in that it enables a stream of messages instead of a stream of bytes.

In other words, there is a persistent connection between client and server, and any of them can start sending data at any time. This way you will think about using WebSockets whenever you need a near real-time connection between the client and the server, whether it is in a web environment or not.

Please note that Nginx supports Websockets starting in version 1.3.13 (released on February 2013) and is accessible within the core product. Older versions DO NOT support this protocol.

In this tutorial we will also configure Upstart, a modern replacement for init.d written by the Ubuntu developers, to make sure that our websocket application (written in Node.js) automatically restarts if it crashes, and starts up when our server boots up.

# ## 6.2 Installing Node.js

First off, let’s create a directory inside our home to download the source code for Node.js (see Fig. 6.1). Note that for the sake of clarity, this directory is located at the same level that the one where we downloaded the source code for Nginx as explained in Tutorial #1. We will then use the same directory to extract the contents of the tarball and to install Node.js using the regular procedure:

(We are following the usual build process here because the checkinstall method produced an error while building the deb package.)

```
sudo ./configure, sudo make, sudo make install
```

At the time of this writing, the latest version of Node.js is v0.10.21, which can be downloaded (32-bit or 64-bit versions) from http://nodejs.org/download/ using the following command (see Fig. 6.2, where the proxy server being used and its IP address have been blurred for privacy reasons):

```
wget http://nodejs.org/dist/v0.10.21/node-v0.10.21.tar.gz
```