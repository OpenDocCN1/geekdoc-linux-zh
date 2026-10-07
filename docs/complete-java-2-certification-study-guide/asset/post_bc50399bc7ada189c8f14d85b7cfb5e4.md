
# Serializable Objects

Not all objects may be serialized, this is not obvious from a casual glance at the API page for ObjectOutputStream. The method summary entry for writeObject() says

```
public void writeObject(Object obj)
```

However, if you look at the method detail section for writeObject(), you'll see that it throws NotSerializableException if “some object to be serialized does not implement the java.io.Serializable interface.” So though the method declares that its argument is an object, code that checks for the precondition that the argument must be an instanceof Serializable and throws the exception if the precondition is not. Even if the object is passed into the method Serializable, the object's entire graph is serialized, all objects referenced by the object must implement Serializable, and all objects referenced by those do the same, and so on.

> Recall from Chapter 5, "Flow Control, Assertions, and Exception Handling," in the discussion on assertions, that assertions should not be used to check conditions in methods. Fortunately, writeObject() respects this rule.

![](img/09f8339b7ae2705d1ab14be2d5e857e3_479_0.png)

You probably recognize the Serializable interface from your reading of the API pages. Most of the core Java classes implement it. All the wrapper classes do so, and so the collection classes. In fact, the only core classes that do not implement Serializable are ones that should not be serialized. For example, it might sense to try to serialize a thread, because a thread's state is tightly bound to the JVM's thread scheduler. It wouldn't be really helpful or meaningful to serialize a thread. Likewise, the low-level output and input streams of the java.io package implement Serializable because they interact with the underlying hardware.

When you create a class that might be serialized, the class should not define any methods at all. All you need to do is type implements java.io.Serializable in your declaration, and you're finished. Empty interfaces such as Serializable are known as tagging interfaces. They identify implementing classes as having certain properties, without requiring those classes to implement any methods. Arrays of primitives or serializable objects are themselves serialized.

Serializable has a subinterface Externalizable, which you can implement if you want to customize the way a class is serialized. Since Externalizable extends Serializable, the implements Serializable precondition in writeObject() is met by any object that implements Externalizable.

Externalizable contains two method signatures:

```
void writeExternal(ObjectOutput out)
throws IOException
void readExternal(ObjectInput in)
throws IOException, ClassNotFoundException
```

# Chapter 13 · Object Streams and RMI

ObjectOutput and ObjectInput are interfaces that are implemented by ObjectOutputStream and ObjectInputStream. They define, respectively, writeObject() and readObject() methods. Implementing Externalizable is useful when you don't trust the environment in which serialized instances of your class will be stored. If you're concerned hostile parties might be able to read sensitive fields of your class, you have the option of encrypting those fields. (You can also choose not to serialize sensitive fields at all, which is more easily accomplished by declaring them to transient.) For example, the following class performs its serialization, protecting the password by reversing it before writing it out.

```
import java.io.*;

public class Account implements Externalizable {
    private String ownerName;
    private String password;
    private float balance;

    private String reverse(String reverseMe) {
        String reversed = "";
        for (int i=reverseMe.length()-1; i>=0; i--)
            reversed += reverseMe.charAt(i);
        return reversed;
    }

    public void writeExternal(ObjectOutput outStream)
        throws IOException {
        outStream.writeObject(ownerName);
        outStream.writeObject(reverse(password));
        outStream.writeObject(new Float(balance));
    }

    public void readExternal(ObjectInputStream inputStream)
        throws IOException, ClassNotFoundException {
        ownerName = (String)inputStream.readObject();
        String reversedPassword = (String)inputStream.readObject();
        password = reverse(reversedPassword);
        balance = ((Float)inputStream.readObject()).floatValue();
    }
}
```

# Sockets and Streams

When an instance of this class is passed to an Object Stream, the default serialization procedure is bypassed; instead, the stream calls the instance's writeExternal() method. When an Object Input Stream reads a serialized instance of Account, a call is made to the no-args constructor for the Account class. Then the newly constructed object receives a readExternal()

Notice that the readObject() mechanism of ObjectInputStream relies on the existence of a no-args constructor for any class that implements Externalizable. If an externalizable class has no no-args constructor, the readObject() method will throw java.io.InvalidClassException.

# Remote Control Using Object Streams

If you decide to use object streams for your project, you will need to build a mechanism for one JVM to tell another JVM what to do. Your client JVM will be displaying the Swing GUI, which will capture commands from the network. The commands will involve retrieving or modifying the contents of the database file, which is under the control of the server JVM.

The straightforward way to build a remote-control system is to create a class that represents a command. The client can issue commands to the server by writing an instance of a command object to an Object Output Stream that is connected to the server. The server can interpret the command object, take appropriate action, and if necessary send some kind of response object back to the client.

In this section we'll develop the code for a very simple remote-control system. We'll create a server that can add and subtract floats on behalf of a client. Of course, the client is perfectly capable of doing its own arithmetic; the goal here is to provide an example that's simple enough that the communication between client and server is clear.

Let's start developing a class that encapsulates a request from the client. We'll call the class Operation. It should contain the Floats to be added or subtracted, as well as a field that specifies what operation should be performed. Without enums, it would probably make sense to use an int to encode the desired operation. But since enums are available, we should make an enum that describes the server's various services:

```
enum Operation {
    ADD, SUBTRACT, DONE;
}
```

In addition to ADD and SUBTRACT, the enum has a DONE value that tells the server that the client is done. On receiving this value, the server can close its streams.

The Command class is straightforward:

```
import java.io.*;
```

```
class Command implements Serializable {
    private Operation operation;
    private float[] operands;
```

```
Command(Operation operation) {
    this.operation = operation;
}
```

```
Command(Operation operation, float[] operands) {
    this.operation = operation;
    this.operands = operands;
}
```

```
Operation getOperation() {
    return operation;
}
```

```
float[] getOperands() {
    return operands;
}
```

Fortunately, enums are serializable, so the Command class' entire graph is serializable. The Server class is an application that creates a server socket on port 7654. (The port number was assigned arbitrarily. Numbers under 1024 are reserved for assignment by a standards committee. The server greater than 1024 are uncontrolled and may be used freely.) a client connection, then spawns a thread to service the connection, and then goes waiting for connections. We'll look first at the Server class and then at the service-providing thread class. Here's the Server class:

```
import java.io.*;
import java.net.*;
```

```
public class Server {
    public static void main(String[] args) {
        ServerSocket ss = new ServerSocket(7654);
        while (true) {
            Socket sock = ss.accept();
            ServiceGiver sg = new ServiceGiver(sock);
            sg.start();
        }
    }
}
```
