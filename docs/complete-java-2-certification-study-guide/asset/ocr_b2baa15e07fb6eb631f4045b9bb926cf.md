# Chapter 9 • I/O Streams

+   5. BufferedOutputStream(raf);
6. DataOutputStream dos = new DataOutputStream(bos);
7. dos.writeDouble(Math.PI);
8. dos.close();
9. bos.close();
10. raf.close();
11. }
12. catch (IOException e) { }

+   13. The code fails to compile.
A. The code compiles but throws an exception
B. The code compiles and executes but has no effect on the local file.
D. The code compiles and executes; afterward, the current working directory contains a file datafile.

+   11. Suppose you are writing a class that will provide custom serialization. The class implements java.io.Serializable (not java.io.Externalizable). What access mode should the writeObject() method have?
A. public
B. protected
C. default
D. private

+   12. Suppose you are writing a class that will provide custom deserialization. The class implements java.io.Serializable (not java.io.Externalizable). What access mode should the readObject() method have?
A. public
B. protected
C. default
D. private

+   13. Suppose class A extends Object; class B extends A; and class C extends B. Of these, only class implements java.io.Serializable. Which of the following must be true in order to avoid an exception during deserialization of an instance of C?
A. A must have a no-args constructor.
B. B must have a no-args constructor.
C. C must have a no-args constructor.
D. There are no restrictions regarding no-args constructors.