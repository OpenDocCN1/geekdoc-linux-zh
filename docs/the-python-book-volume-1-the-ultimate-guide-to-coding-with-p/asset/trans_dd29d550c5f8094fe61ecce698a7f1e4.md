

## 使用 Python

### 我们需要告诉 GObject 我们将使用线程

```
def handle_msg(self, data):
    # Print and then process the message we've just received
    print "{0} sent: {1}".format(self.address, data)
    # Use regular expressions to test for a message like "USERNAME liam"
    username_result = re.search("USERNAME (.*)", data)
    if username_result:
        self.username = username_result.group(1)
        self.server.echo("{0} has joined.\n".format(self.username))
    elif data == "QUIT":
        # If the client has sent quit then close this thread
        self.quit()
    elif data == "":
        # The socket at the other end is probably closed
        self.quit()
    else:
        # It's a normal message so echo it to everyone
        self.server.echo(data)
```

```
#!/usr/bin/env python2
# The client side of an instant messaging application. Written as part of a Linux User & Developer tutorial by Liam Fraser in 2013.

import threading
import gtk
import gobject
import socket
import re
import time
import datetime

# Tell gobject to expect calls from multiple threads
gobject.threads_init()
```

### 11 启动服务器

实际启动 Server 类的代码如下。注意你最好选择一个高编号的端口，因为打开 <1024 的端口需要 root 权限。

```
if __name__ == "__main__":
    # Start a server on port 59091
    server = Server(59091)
    server.run()
```

### 12 客户端

像为服务器创建新文件一样为客户端创建一个新文件并在你喜欢的编辑器中打开它。客户端需要与服务器相同的导入，以及 gtk、gobject 和 datetime 库。我们需要做的一件重要事情是告诉 GObject 我们将使用线程，这样我们就可以从其他线程调用函数，并且主窗口在主 GTK 线程中运行，可以更新。

### 13 客户端图形用户界面

客户端的用户界面不是本教程的重点，也不会像其余代码那样详细解释。然而，代码应该相当容易阅读，我们提供了链接到文档以帮助你。

我们的 MainWindow 类继承自 gtk Window 类，因此我们需要首先使用 super 关键字初始化它。然后我们创建将放在窗口上的控件，将它们的事件连接到函数，最后按我们想要的方式布局控件。destroy 事件在程序关闭时触发，其他事件应该显而易见。

GTK 使用打包布局，其中你使用 VBoxes 和 HBoxes 来布局控件。V 和 H 代表垂直和水平。这些控件本质上让你像表格一样分割窗口，并且会根据应用程序的大小自动决定控件的大小。

GTK 没有提供输入基本信息（如服务器 IP 地址、端口和你选择的用户名）的控件，因此我们制作了一个名为 ask_for_info 的函数，它创建一个消息框，向其中添加一个文本框，然后检索结果。我们这样做是因为它更简单，使用代码更少，而不是创建一个新窗口来接受信息。

```
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
        text_view = gtk.TextView(self.text_buffer)
        # Connect events
        self.connect("destroy", self.graceful_quit)
        send_button.connect("clicked", self.send_message)
        # Activate event when user presses Enter
        self.text_entry.connect("activate", self.send_message)
        # Do layout
        vbox.pack_start(text_view)
        hbox.pack_start(self.username_label, expand = False)
        hbox.pack_start(self.text_entry)
        hbox.pack_end(send_button, expand = False)
        vbox.pack_end(hbox, expand = False)
        # Show ourselves
        self.add(vbox)
        self.show_all()
        # Go through the configuration process
        self.configure()
```

### 14 配置客户端

这段代码在我们将控件添加到主窗口后运行，并向用户请求输入。目前，如果用户输入错误的服务器地址或端口，应用程序将退出，但这不是生产系统，所以没关系。

```
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

    def configure(self):
        # Performs the steps to connect to the server
        # Show a dialog asking for server address followed by a port
        server = self.ask_for_info("server_address:port")
        # Regex that crudely matches an IP address and a port number
        regex = re.search(r"(\d+\.\d+\.\d+\.\d+):(\d+)", server)
        address = regex.group(1).strip()
        port = regex.group(2).strip()
        # Ask for a username
        self.username = self.ask_for_info("username")
        self.username_label.set_text(self.username)
        # Attempt to connect to the server and then start listening
        self.network = Networking(self, self.username, address, int(port))
        self.network.listen()
```

### 15 MainWindow 的其余部分

MainWindow 类的其余部分有大量注释来解释其自身，如下所示。需要注意的一点是，当客户端发送消息时，它不会立即在文本视图中显示。服务器会将消息回显给每个客户端，因此客户端只是在服务器回显回来时才显示自己的消息。这意味着当你看不到自己发送的消息时，你可以判断服务器没有接收到你的消息。

```
def add_text(self, new_text):
    # Add text to the text view
    text_with_timestamp = "{0} {1}".format(datetime.datetime.now(), new_text)
    # Get the position of the end of the text buffer, so we know where to insert new text
    end_iter = self.text_buffer.get_end_iter()
    # Add new text at the end of the buffer
    self.text_buffer.insert(end_iter, text_with_timestamp)
```

```
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

> 服务器会将消息回显给每个客户端

![](img/3b256f430f51c98f1315671f6e4eec19_91_0.png)

