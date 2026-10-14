
## Instant messaging with Python

How to program both the client, complete with a GUI, and server of a simple instant messenger in Python

## Resources

- A computer - running your favourite Linux distribution
- Internet connection - to access documentation
- Python 2.x, PyGTK and GObject - packages installed

Here we'll be implementing an instant messenger in Python with a client-server architecture. This means each client connects to the server, which relays any message that one client sends to all other clients. The server will also notify the other clients when someone joins or leaves the server. The instant messenger can work anywhere a TCP socket can: on the same computer with the loopback interface, across various computers on a LAN, or even over the internet if you were to configure your router correctly. However, our messages aren't encrypted, so we wouldn't recommend that.

Writing an instant messenger is an interesting technical problem that covers a bunch of areas that you may not have come across while programming before:

- We'll be employing sockets, which are used to transmit data across networks.
- We'll also be using threading, which allows a program to do multiple things at once.
- We'll cover the basics of writing a simple graphical user interface with GTK, as well as how to interact with that from a different thread.
- Finally, we'll be touching on the use of regular expressions to easily analyse and extract data from strings.

Before getting started, you'll need to have a Python 2.x interpreter installed, as well as the PyGTK bindings and the Python 2 GObject bindings. The chances are that if you have a system with a fair amount of software on it, you will already have these packages, so it may be easier to wait and see if you're missing any libraries when you attempt to import them. All of the above packages are commonly used, so you should be able to install them using your distro's package manager.

Each message has a time stamp prefixed to it

A client can detect when the server exits without crashing or hanging

The server notifies all clients when a new client joins

Similarly, the server notifies all clients when a client leaves

## 01 The server

The server will do the following jobs:

- Listen for new clients
- Notify all clients when a new client joins
- Notify all clients when a client leaves
- Receive and deliver messages to all clients

We're going to write the server side of the instant messenger first, as the client requires it. There will be two code files, so it's a good idea to make a folder to keep them inside. You can create an empty file with the command `touch [filename]` and mark that file as executable using `chmod +x [filename]`. This file is now ready to edit in your favourite editor.

```
[liam@liam-laptop Python]$ mkdir Python-IM
[liam@liam-laptop Python]$ cd Python-IM/
[liam@liam-laptop Python-IM]$ touch IM-Server.py
[liam@liam-laptop Python-IM]$ chmod +x IM-Server.py
```

## 02 Starting off

As usual, we need to start off with the line that tells the program loader what it needs to interpret the rest of the file with. In our case, that line is:

```
#!/usr/bin/env python2
```

On your system, it may need to be changed to `#!/usr/bin/env python2.6` or `#!/usr/bin/env python2.7`.

After that, we've written a short comment about what the application does, and imported the required libraries. We've already mentioned what the threading and socket libraries are for. The `re` library is used for searching strings with regular expressions. The `signal` library is used for dealing with signals that will kill the program, such as SIGINT. SIGINT is sent when Ctrl+C is pressed. We handle these signals so that the program can tell the clients that it's exiting rather than dying unexpectedly. The `sys` library is used to exit the program. Finally, the `time` library is used to put a sensible limit on how frequently the body of while loops executes.

```
#!/usr/bin/env python2
# The server side of an instant messaging application. Written as part of a Linux User & Developer tutorial by Liam Fraser in 2013.
import threading
import socket
import re
import signal
import sys
import time
```

## 03 The Server class

The Server class is the main class of our instant messenger server. The initialiser of this class accepts a port number to start listening for clients on. It then creates a socket, binds the socket to the specified port on all interfaces, and then starts to listen on that port. You can optionally include an IP address in the tuple that contains the port. Passing in a blank string like we have done causes it to listen on all interfaces. The value of 1 passed to the `listen` function specifies the maximum number of queued connections we can accept. This shouldn't be a problem as we're not expecting a bunch of clients to connect at exactly the same time.

Now that we have a socket, we'll create an empty array that will be later used to store a collection of client sockets that we can echo messages to. The final part is to tell the signal library to run the `self.signal_handler` function, which we have yet to write, when a SIGINT or SIGTERM is sent to the application so that we can tidy up nicely.

```
class Server():
    def __init__(self, port):
        # Create a socket and bind it to a port
        self.listener = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
        self.listener.bind(('', port))
        self.listener.listen(1)
        print "Listening on port {0}".format(port)
        # Used to store all of the client sockets we have, for echoing messages to them
        self.client_sockets = []
        # Run the function self.signal_handler when Ctrl+C is pressed
        signal.signal(signal.SIGINT, self.signal_handler)
        signal.signal(signal.SIGTERM, self.signal_handler)
```

## 04 The server's main loop

The server's main loop accepts new connections from clients, adds that client's socket to the collection of sockets and then starts an instance of the ClientListener class, which we have yet to write, in a new thread. Sometimes, defining interfaces you are going to call before you've written them is good, because it can give an overview of how the program will work without worrying about the details.

### Useful documentation

- Threading: docs.python.org/2/library/threading.html
- Sockets: docs.python.org/2/library/socket.html
- Regular expressions: docs.python.org/2/library/re.html
- The signal handler: docs.python.org/2/library/signal.html
- PyGTK: www.pygtk.org/pygtk2reference.html
- GObject: www.pygtk.org/pygtk2reference/gobject-functions.html

Note that we're printing information as we go along, to make debugging easier should we need to do it. Sleeping at the end of the loop is useful to make sure the while loop can't run quickly enough to hang the machine. However, this is unlikely to happen as the line that accepts new connections is blocking, which means that the program waits for a connection before moving on from that line. For this reason, we need to enclose the line in a try block, so that we can catch the socket error and exit when we can no longer accept connections. This will usually be when we've closed the socket during the process of quitting the program.

```
def run(self):
    while True:
        # Listen for clients, and create a ClientThread for each new client
        print "Listening for more clients"
        try:
            (client_socket, client_address) = self.listener.accept()
        except socket.error:
            sys.exit("Could not"
```
