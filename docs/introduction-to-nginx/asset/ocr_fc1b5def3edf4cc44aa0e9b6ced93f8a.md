![](bbox=[0.08, 0.07, 0.95, 0.2])

![](bbox=[0.08, 0.2, 0.95, 0.42])

# ## 6.3 Installing additional libraries

Next, we will install `socket.io`, which is a JavaScript library for real-time web applications. It has two parts:

+   - a client-side library that runs in the browser and
+   - a server-side library for node.js (Socket.io, Wikipedia) using npm (the offcial package manager for node.js, sudo npm install socket.io, see Fig. 6.3), and express, a web application framework for node.js.

![](bbox=[0.08, 0.59, 0.95, 0.73])

To download the express framework we need to define a couple of settings in a json file (package.json) located in a directory created for our application - ~/chatroom in this example- (see Fig. 6.4). Then we proceed to download and install it with:

```
npm install -d
```