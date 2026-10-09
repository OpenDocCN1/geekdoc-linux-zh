```
InputStream i = s.getInputStream();        // Get input stream
OutputStream o = s.getOutputStream();       // Get output stream
String str;
do
{
    byte[] line = new byte[100];
    System.in.read(line);                    // Read from console
    o.write(line);                           // Send the message
    i.read(line);                            // Read it back
    str = new String(line);                  // Convert to string
    System.out.println(str.trim());          // Print message
}
while (!str.trim().equals("bye"));
s.close();                                 // Close connection
```

**Listing 12.1** shows a simple reading and sending loop. It is far from complete, but it demonstrates the functionality. If you try to compile this snippet, the compiler complains about not catching certain exceptions. All network operations must capture exceptions. For the source, **Listing 12.1**, you surround the code with the following:

```
try
{
// <--Add all source here
}
catch (Exception err)
{
    System.err.println(err);
}
```

The try...catch block completes the example. You can drop this code directly in a main() block of a class.

# ### Java TCP Servers

As you saw in the earlier sections, Java has simplified creating, reading, writing, and closing sockets. Writing the corresponding server is even easier. The call to create a server socket has three interfaces:

```
ServerSocket s = new ServerSocket(int PortNum);
ServerSocket s = new ServerSocket(int PortNum, int Backlog);
ServerSocket s = new ServerSocket(int PortNum, int Backlog,
                                  InetAddress BindAddr);
```

The **Backlog** and **BindAddr** offer the same features as the C-based system calls listen() (awaiting-connection queue) and bind() (to a specific network interface).

If you recall, a C-based server program takes about 7–10 lines to write. In Java, you can create an equivalent server in about two lines:

```
ServerSocket s = new ServerSocket(9999);
Socket c = s.accept();
```