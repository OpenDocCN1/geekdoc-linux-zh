
# Work with Python

```python
hbox.pack_start(self.text_entry)
hbox.pack_end(send_button, expand = False)
vbox.pack_end(hbox, expand = False)
# Show ourselves
self.add(vbox)
self.show_all()
# Go through the configuration process
self.configure()
def ask_for_info(self, question):
# Shows a message box with a text entry and returns the response
dialog = gtk.MessageDialog(parent = self, type = gtk.MESSAGE_QUESTION,
flags = gtk.DIALOG_MODAL |
gtk.DIALOG_DESTROY_WITH_PARENT,
buttons = gtk.BUTTONS_OK_CANCEL,
message_format = question)
entry = gtk.Entry()
entry.show()
dialog.vbox.pack_end(entry)
response = dialog.run()
response_text = entry.get_text()
dialog.destroy()
if response == gtk.RESPONSE_OK:
    return response_text
else:
    return None
```

```python
def configure(self):
# Performs the steps to connect to the server
# Show a dialog box asking for server address followed by a port
server = self.ask_for_info("server address:port")
# Regex that crudely matches an IP address and a port number
regex = re.search('^(\d+\.\d+\.\d+\.\d+):(\d+)$', server)
address = regex.group(1).strip()
port = regex.group(2).strip()
# Ask for a username
self.username = self.ask_for_info("username")
self.username_label_set_text(self, self.username)
# Attempt to connect to the server and then start listening
self.network = Networking(self, self.username, address, int(port))
self.network.listen()
```

## Configuring the client

This code is run after we've added the controls to the main window, and asks the user for input. Currently, the application will exit if the user enters an incorrect server address or port; but this isn't a production system, so that's fine.

## The remainder of MainWindow

The rest of the **MainWindow** class has plenty of comments to explain things, so I won't go through those as follows. One thing to note is that when a client sends a message, it doesn't display it in the text view straight away. The server is going to echo the message to each client, so the client simply displays its own message when the server echoes it back. This means that you can tell if the server is not receiving your messages when you don't see a message that you send.

```python
def add_text(self, new_text):
# Add text to the text view
text_with_timestamp = "{0} [1]".format(datetime.datetime.now())
new_text()
# Get the position of the end of the text buffer, so we know where to insert new text
end_itr = self.text_buffer.get_end_iter()
# Add new text at the end of the buffer
self.text_buffer.insert(end_itr, text_with_timestamp)
def send_message(self, widget):
# Clear the text entry and send the message to the server
# We don't need to display it as it will be echoed back to each client, including us.
new_text = self.text_entry.get_text()
self.text_entry.set_text("")
message = "{0} says: {1}\n".format(self.username, new_text)
self.network.send(message)
def graceful_quit(self, widget):
# When the application is closed, tell GTK to quit, then tell the server we are quitting and tidy up the network
gtk.main_quit()
self.network.send("QUIT")
self.network.tidy_up()
```

![](img/e016e192a91ffc1a9e474690a590742f_87_0.png)

> “The server is going to echo the message to each client”

**16 The client’s Networking class**

Much of the client's **Networking** class is similar to that of the server’s. One difference is that the class doesn't inherit the **Thread** class – we just start one of its functions as a thread.

```python
class Networking():
    def __init__(self, window, username, server, port):
        # Set up the networking class
        self.window = window
        self.socket = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
        self.socket.connect((server, port))
        self.listening = True
        # Tell the server that a new user has joined
        self.send("USERNAME {0}".format(username))

    def listener(self):
        # A function run as a thread that listens for new messages
        while self.listening:
            data = ""
            try:
                data = self.socket.recv(1024)
            except socket.error:
                "Unable to receive data"
            self.handle_msg(data)
        # Don't need the while loop to be ridiculously fast
        time.sleep(0.1)
```

**17 Running a function as a thread**

The listener function above will be run as a thread. This is trivial to do. Enabling the **daemon** option on the thread means that it will die if the main thread unexpectedly ends.

```python
def listener(self):
    # Start the listening thread
    self.listen_thread = threading.Thread(target=self. listener)
    # Stop the child thread from keeping the application open
    self.listen_thread.daemon = True
    self.listen_thread.start()
```

**18 Finishing the Networking class**

Again, most of this code is similar to the code in the server's Networking class. One difference is that we want to add some things to the text view of our window. We do this by using the **idle_add** function of GObject. This allows us to call a function that will update the window running in the main thread when it is not busy.

```python
def send(self, message):
    # Send a message to the server
    print "Sending: {0}".format(message)
    try:
        self.socket.sendall(message)
    except socket.error:
        print "Unable to send message"

    def tidy_up(self):
        # We'll be tidying up if either we are quitting or the server is quitting
        self.listening = False
        self.socket.close()
        # We won't see this if it's us that's quitting as the window will be gone shortly
        gobject.idle_add(self.window.add_text, "Server has quit.\n")

def handle_msg(self, data):
    if data == "QUIT":
        # Server is quitting
        self.tidy_up()
    elif data == "":
        # Server has probably closed unexpectedly
        self.tidy_up()
    else:
        # Tell the GTK thread to add some text when it's ready
        gobject.idle_add(self.window.add_text, data)
```

**19 Starting the client**

The main window is started by initialising an instance of the class. Notice that we don't need to store anything that is returned. We then start the GTK thread by calling **gtk.main()**.

```python
if __name__ == "__main__":
    # Create an instance of the main window and start the gtk main loop
    MainWindow()
    gtk.main()
```

**20 Tryying it out**

You'll want a few terminals: one to start the server, and some to run clients. Once you've started the server, open an instance of the client and enter **127.0.0.1**:port, where 'port' is the port you decided to use. The server will print the port it's listening on to make this easy. Then enter a username and click OK. Here is an example output from the server with two clients. You can use the client over a network by replacing 127.0.0.1 with the IP address of the server. You may have to let the port through your computer's firewall if it is not working.

```
[liam@liam-laptop19 Python]$ .\IM-Server.py
Listening on port 59891
Listening for more clients
Starting client thread for ('127.0.0.1', 38726)
sent: USERNAME client1
echoing: client1 has joined.
Listening for more clients
Starting client thread for ('127.0.0.1', 38739)
sent: USERNAME client2
echoing: client2 has joined.
Listening for more clients
Starting client thread for ('127.0.0.1', 38739)
sent: Hi
echoing: client1 says: Hi
echoing: client2 says: client1 says: Hi
echoing: client1 says: Quit
echoing: client1 has quit.
Ending client thread for ('127.0.0.1', 38726)
^C
echoing: QUIT
Could not accept any more connections
ending client thread for ('127.0.0.1', 38739)
sent: echoing: client2 has quit.
```

**21 That's it!**

So... it's not perfect and could be a little more robust in terms of error handling, but we have a working instant messenger server that can accept multiple clients and relay messages between them. More importantly, we have learned a bunch of new concepts and methods of working.
