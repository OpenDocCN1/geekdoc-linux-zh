
```java
}
catch (IOException x) {
    System.out.println("Server Stress: " +
    x.getMessage());
}
```

There is nothing difficult about the Server class. Its main() is structured just like the example in the Server Socket discussion earlier in this chapter, in the "Sockets in Java" section. There is nothing in the code to indicate what kind of service is performed, and with a good sign: it indicates that functionality is nicely partitioned. The Server class takes care of establishing connections, while the ServiceGiver class provides service on those connections. Here is the ServiceGiver code:

```java
import java.io.*;
import java.net.*;
```

```java
class ServiceGiver extends Thread {
    private Socket sock;

    ServiceGiver(Socket sock) {
        this.sock = sock;
    }

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
                    case SUBTRACT:
                        result = operands[0] - operands[1];
                        oos.writeObject(result);
                        break;
                    case DONE:
                        oos.close();
                        ois.close();
                        os.close();
                        is.close();
                        sock.close();
                        return;
                }
            }
        } catch (IOException x) {
            System.out.println("IO Stress: " + x.getMessage());
        } catch (ClassNotFoundException x) {
            System.out.println("Class Stress: " + x.getMessage());
        }
    }
}
```

This catch follows the structure of the example given earlier in this chapter, in the “Server Sockets in Java” section. It was suggested that a service-providing class should implement Runnable. In the example the code is quite simple, so it's sufficient to extend Thread. The constructor creates the socket that is to receive service. All service takes place in the run() method, which loops on reading a Command object from the input stream, extracting the Operation from the Command object, and taking appropriate action. Recall that Operation is an enum, so here you see an example of switching on an enum value.

Let's finish this example by looking at a simple client that connects to a server and then commands the server to perform each of its operations:

```java
import java.io.*;
import java.net.*;

public class Client {
    public static void main(String[] args) {
        try {
            test(args[0]); // server name
        } catch (IOException x) {
            System.out.println("IO Stress: " + x.getMessage());
        } catch (ClassNotFoundException x) {
            System.out.println("Class Stress: " + x.getMessage());
        }
    }

    private static void test(String serverName)
        throws IOException, ClassNotFoundException {
        // Connect to server.
        Socket sock = new Socket(serverName, 7654);

        // Build object streams.
        OutputStream os = sock.getOutputStream();
        ObjectOutputStream oos = new ObjectOutputStream(os);
        InputStream is = sock.getInputStream();
        ObjectInputStream ois = new ObjectInputStream(is);

        // Test addition.
        float[] addUs = {12.3f, 56.7f};
        Command command = new Command(Operation.ADD, addUs);
        oos.writeObject(command);
        Float result = (Float)ois.readObject();
        System.out.println("Addition result: " + result);

        // Test subtraction.
        float[] subtractUs = {3.14159f, 1.11111f};
        command = new Command(Operation.SUBTRACT, subtractUs);
        oos.writeObject(command);
        result = (Float)ois.readObject();
        System.out.println("Subtraction result: " + result);

        // Done.
        command = new Command(Operation.DONE);
        oos.writeObject(command);
        oos.close();
        ois.close();
        os.close();
        is.close();
        sock.close();
    }
}
```

The Client application assumes that the server’s hostname is supplied on the command line. The main() method calls test(), which commands the server to add, then subtract, and then be done.

The server and client are able to function together because each is aware of the other’s requirements and behavior. These define a little protocol, which can be summarized as follows:

- 1. The client initiates communication, by sending a Command instance to the server.
- 2. When the server receives an ADD or SUBTRACT command, it responds with a float.
- 3. When the server receives a DONE command, it closes the connection without responding.

If you decide to use object streams for your project, your project will be much more intricate than the one you chose, but its structure will be similar: the client will initiate communication sending something to the server, which will do something with the database and then send a response.

So far in what you’ve seen how object streams are a good foundation for a system in which a client gives orders to.
