The package has several other classes that really don't fit in this classification. An example is SequenceInputStream, which allows you to merge two streams into one.

Of all these classes, you may want to familiarize yourself most with ObjectInputStream and ObjectOutputStream for sending and receiving custom classes or BufferedReader and PrintWriter for string I/O. Network programs often use these because they suit socket programming the best. Similarly, you can use the ByteArrayOutputStream or ByteArrayOutputStream objects to provide interfaces for datagram messages.

# # Converting Between I/O Classes

Some features that one class owns may not be directly available in the I/O class that the socket hands you. The Socket class only offers two I/O classes—OutputStream and InputStream. These offer pretty much bare bones reading and writing of byte arrays. To get the different features, you need to convert these classes.

Suppose you want to read in strings, not byte arrays. The BufferedReader has a good String interface. You need to convert from the InputStream abstract class to the Reader abstract class. The InputStreamReader class acts as the go-between for this conversion:

```
```
Socket s = new Socket(host, port);
InputStream is = s.getInputStream();
InputStreamReader isr = new InputStreamReader(is);
BufferedReader br = new BufferedReader(isr);
String l = br.readLine();
```
```

You can also use the following customary shorthand:

```
```
BufferedReader br = new BufferedReader(new InputStreamReader(
s.getInputStream()));
```
```

Sending a string (without actually converting the string) through a channel is a little easier:

```
```
String msg = new String( 
"<html><body>Welcome to my Java website</body></html>");
SocketServer ss = new SocketServer(9999);
Socket s = ss.accept();
PrintWriter pw = new PrintWriter(s.getOutputStream(), true);
pw.println(msg);
s.close();
```
```

The first parameter gives the new PrintWriter instance a reference to the socket's stream. The second parameter tells the object to autorefush whenever the program calls println(). Normally, the I/O in PrintWriter buffers up the data until it has enough to minimize band-width waste. Specifying autoflush says that you want to specify when a buffer is sent.