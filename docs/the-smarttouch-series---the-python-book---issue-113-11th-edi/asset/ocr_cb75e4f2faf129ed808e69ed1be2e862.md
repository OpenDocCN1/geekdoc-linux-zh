# We need to tell Gobject that we'll be using threading

```
```python
def handle_msg(self, data):
    # Print and then process the message we've just received
    print('{0} sent: {1}'.format(self, data))
    
    # Use regular expressions to test for a message like "USERNAME_ Liam"
    username_result = re.search('^USERNAME_(.*$)', data)
    if username_result:
        self.username = username_result.group(1)
        self.server.echo('({0} has joined. An'.format(self, username))
    elif data == "QUIT":
        # If the client has sent quit then close this thread
        self.quit()
        self.data = ""
        # The socket at the other end is probably closed
        self.quit()
    else:
        # It's a normal message so echo it to everyone
        self.server.echo(data)
```
```

# 11

Starting the server

The code that actually starts the Server class is as follows. Note that you are probably best picking a high-numbered port as you need to be root to open ports <1024.

```
```python
if __name__ == "__main__":
    # Start a server on port 59091
    server = Server(59091)
    server.run()
```
```

# 12

The client

Create a new file for the client as we did for the server and open it in your favourite editor. The client requires the same imports as the server, as well as the gtk, gobject and datetime libraries. One important thing we need to do is to tell GObject that we'll be using threading, so we can call functions from other threads and have the main window, which is running in the main GTK thread, update.

```
```bash
#!/usr/bin/env python2
# The client side of an instant messaging application. Written as part of a Linux User & Developer tutorial by Liam Fraser in 2013.

import threading
import gtk
import gobject
import socket
import re
import time
import datetime
```
```

```
```python
# Tell gobject to expect calls from multiple threads
gobject.threads_init()
```
```

# 13

The client graphical user interface

The user interface of the client isn't the main focus of the tutorial, and won't be explained in as much detail as the rest of the code. However, the code should be fairly straightforward to read and we have provided links to documentation that will help.

Our MainWindow class inherits the gtk.Window class, so we need to start by initialising that using the super keyword. Then we create the controls that will go on the window, connect any events they have to functions, and finally lay out the controls how we want. The destroy event is raised when the program is closed, and the other events should be obvious.

GTK uses a packing layout, in which you use Vboxes and Hboxes to lay out the controls. V and H stand for vertical and horizontal. These controls essentially let you split a window up almost like a table, and will automatically decide the size of the controls depending on the size of the application. GTK doesn't come with a control to enter basic information, such as the server's IP address, port and your chosen username, so we've made a function called ask_for_info, which creates a message box, adds a text box to it and then retrieves the results. We've done this because it's simpler and uses less code than creating a new window to accept the information.

```
```python
class MainWindow(gtk.Window):
    def __init__(self):
        # Initialise base gtk window class
        super(MainWindow, self).__init__()
        
        # Create controls
        self.set_title("IM Client")
        vbox = gtk.VBox()
        hbox = gtk.HBox()
        self.username_label = gtk.Label()
        
        self.text_entry = gtk.Entry()
        send_button = gtk.Button("Send")
        self.text_buffer = gtk.TextBuffer()
        text_view = gtk.TextView(self, text_buffer)
        
        # Connect events
        self.connect("destroy", self.graceful_quit)
        send_button.connect("clicked", self.send_message)
        
        # Activate event when user presses Enter
        self.text_entry.connect("activate", self.send_message)
        
        # Do layout
        vbox.pack_start(text_view)
        hbox.pack_start(self.username_label, expand = False)
```
```