The `Backlog` and `BindAddr` offer the same features as the C-based system calls `listen()` (awaiting-connection queue) and `bind()` (to a specific network interface).

If you recall, a C-based server program takes about 7–10 lines to write. In Java, you can create an equivalent server in about two lines:

```
```java
ServerSocket s = new ServerSocket(9999);
Socket c = s.accept();
```
```

And, like the C-style listening socket, you use the `ServerSocket` for only awaiting client connections. When a client requests a connection, the server gets a new `Socket` object that it can use to create the I/O streams.

Again, you can use these classes to create a `SimpleEchoServer` (see Listing 12.2)

# **LISTING 12.2 The Simple Echo Server in Java Uses Byte Arrays in the Input/Output Streams**

```
```java
//***********************************************
// SimpleEchoServer excerpt
//***********************************************
try
{
    ServerSocket s = new ServerSocket(9999); // Create server
    while (true)
    {
        Socket c = s.accept();       // Await connection
        InputStream i = c.getInputStream(); // Get input stream
        OutputStream o = c.getOutputStream();//Get output stream
        do
        {
            byte[] line = new byte[100]; // Create scratchpad
            i.read(line);        // Read client's message
            o.write(line);       // Send it back
        }
        while ( !str.trim().equals("bye") );
        c.close();              // Close connection
    }
}
catch (Exception err)
{
    System.err.println(err);
}
```
```

Listing 12.2 demonstrates how easy creating a server is in Java. These examples are sketchy and tend to be a little clunky, but the following sections fix the I/O limitations and can help you with more solid code.