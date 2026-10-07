The thread that calls accept() is almost always waiting for new client connections; it is unavailable only for the brief time required to pass a newly connected socket to a ServiceGiver instance.

# Object Streams and Serialization

As you have seen, data streams allow you to read and write primitives and strings, rather than individual bytes. Object streams go one step beyond data streams by allowing you to read and write entire objects.

The process of writing an object is called serialization. To serialize an object, first create an instance of java.io.ObjectOutputStream. This class, like DataOutputStream, expects to be chained onto a lower-level byte-oriented stream as a file output stream or a socket's output stream. The method uses an object stream to store a string buffer in a file named sbuf.

```
void writeString(StringBuffer writeMe)
throws IOException {
FileOutputStream fos = new FileOutputStream("sbuf.ser");
ObjectOutputStream oos = new ObjectOutputStream(fos);
oos.writeObject(writeMe);
oos.close();
fos.close();
}
```

The .ser filename is conventional for files containing serialized objects. To read the stored object back into a program, you can do with the following:

```
StringBuffer readString())
throws IOException, ClassNotFoundException {
FileInputStream fis = new FileInputStream("sbuf.ser");
ObjectInputStream ois = new ObjectInputStream(fis);
StringBuffer sb = (StringBuffer)ois.readObject();\ois.close();
fis.close();
return sb;
}
```

Notice that the value returned by readObject() is of type Object, so it must be cast. The object read is identical to the one that was written out in the previous code example. The ObjectOutputStream class has a writeUTF() method, as well as writeByte(), writeShort(), and all other write-primitive methods that also appear in data output streams. The ObjectInputStream class has corresponding reading methods. If you want to create a file that contains serialized primitives and strings as well as serialized objects, you can do it with a single output stream.