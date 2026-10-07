14. ObjectStreamException extends IOException NotSerializableException extends ObjectStreamException. AWTException does not extend any of these. All are checked exceptions. The callMe() method throws NotSerializableException.What does the following code print? Choose all lines that are printed.

```
try {
  callMe();
  System.out.println("I throw");
}
 catch (ObjectStreamException x) {
  System.out.println("Object stream");
}
 catch (IOException x) {
  System.out.println("IO");
}
 catch (Exception x) {
  System.out.println("Exception");
}
finally {
  System.out.println("Finally");
}
```

+   A. I throw

+   B. Object Stream

+   C. IO

+   D. Exception

+   E. Finally

15. While testing some code that you are developing, you notice that an ArrayIndexOutOfBoundsException is thrown. What is the appropriate reaction?

+   A. Enclose the offending code in a try block, with a catch block for ArrayIndexOutOfBoundsException that does nothing.

+   B. Enclose the offending code in a try block, with a catch block for ArrayIndexOutOfBoundsException that prints out a descriptive message.

+   C. Declare the method that contains the offending code throws ArrayIndexOutOfBoundsException.

+   D. None of the above.