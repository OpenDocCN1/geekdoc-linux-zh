# Work with Python

```
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
```

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
```

# Configuring the client

This code is run after we've added the controls to the main window, and asks the user for input. Currently, the application will exit if the user enters an incorrect server address or port; but this isn't a production system, so that's fine.

# The remainder of MainWindow

The rest of the **MainWindow** class has plenty of comments to explain things, so I won't go through those as follows. One thing to note is that when a client sends a message, it doesn't display it in the text view straight away. The server is going to echo the message to each client, so the client simply displays its own message when the server echoes it back. This means that you can tell if the server is not receiving your messages when you don't see a message that you send.

```
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
```

![](bbox=[0.03, 0.55, 0.4, 0.99])

> “The server is going to echo the message to each client”