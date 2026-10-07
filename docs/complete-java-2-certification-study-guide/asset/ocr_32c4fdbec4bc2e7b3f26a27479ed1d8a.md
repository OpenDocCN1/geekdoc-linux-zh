```
}
catch (IOException x) {
    System.out.println("Server Stress: " +
    x.getMessage());
}

```

There is nothing difficult about the Server class. Its main() is structured just like the example in the Server Socket discussion earlier this chapter, in the "Sockets in Java" section. There is nothing in the code to indicate what kind of service is performed, and with a good sign: it indicates that functionality is nicely partitioned. The Server class takes care of establishing connections, while the ServiceGiver class provides service on those connections. Here is the ServiceGiver code:

```
import java.io.*;
import java.net.*;
```

```
class ServiceGiver extends Thread {
    private Socket sock;

```

```
ServiceGiver(Socket sock) {
    this.sock = sock;
}
```

```
public void run() {
    try {
        // Build object streams.
        OutputStream os = sock.getOutputStream();
        ObjectOutputStream oos = new ObjectOutputStream(os);
        InputStream is = sock.getInputStream();
        ObjectInputStream ois = new ObjectInputStream(is);

        // Provide service.
        while (true) {
            Command command = (Command)ois.readObject();
            float[] operands = command.getOperands();
            switch (command.getOperation()) {
                case ADD:
                    Float result = operands[0] + operands[1];
                    oos.writeObject(result);
                    break;
```