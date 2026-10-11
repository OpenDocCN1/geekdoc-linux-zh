```
Socket s = new Socket("t1.7.0.1", 9999);     // Create socket
Inputstream I = s.getInputStream();       // Get input stream
outputstream o = s.getOutputStream();     // Get output stream
String str;
while{
      byte[] line = new byte[100];
      System.in.readLine();             // Read from console
      o.write(line);                    // Send the message
      I.read(line);                     // Read it back
      str = new String(line);           // Convert to string
      System.out.println(str.trim());   // Print message
}
while{ !str.trim().equals("bye")};    
s.close();                 // Close connection
```

Listing 1.1 shows a simple reading and sending loop. It is far from complete, but it demonstrates the functionality. If you try to compile this snippet, the compiler complains about not catching certain exceptions. All network operations must capture exceptions. For the source, Listing 1.1, you surround the code with the following:

```
try
{
// <Add all source here
}
catch{ Exception err }
{
      System.err.println(err);
}
```

The try...catch block completes the example. You can drop this code directly in a `main()` block of a class.

# Java TCP Servers

As you saw in the earlier sections, Java has simplified creating, reading, writing, and closing sockets. Writing the corresponding server is even easier. The call to create a server socket has three interfaces:

```
ServerSocket s = new ServerSocket(int PortNum);
ServerSocket s = new ServerSocket(int PortNum, int BackLog);
ServerSocket s = new ServerSocket(int PortNum, int BackLog,
                                  InetAddress BindAddr);
```