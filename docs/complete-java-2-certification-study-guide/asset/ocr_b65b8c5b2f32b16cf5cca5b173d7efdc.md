# Strings 261

The Java compiler treats the previous code as if it were the following:

```
new
StringBuilder().append(a).append(b).append(c).toString();
```

If any of the variables (a, b, or c) is a primitive, the append() method computes an appropriate string representation. For an object, the append() method uses the string returned from calling toString() on it. The conversion begins with an empty buffer, then appends each element in turn to the buffer, and finally calls toString() to convert the buffer to a string.

The following code implements a class with its own toString() method:

+   1. class Ab {
2. private int a;
3. private int b;
4. private int c;
5.
6. Abc(int a, int b, int c) {
7. this.a = a;
8. this.b = b;
9. this.c = c;
10. }
11.
12. public String toString() {
13. return "a = " + a + ", b = " + b + ", c = " + c + ";
14. }
15. }

Now the toString() method concatenation (lines 12–14) can be used by any code that wants to take advantage of string concatenation. For example:

```
Abc theAb = new Abc("Here it is: " + theAbc);
System.out.println("Here it is: a = " + a + ", b = " + b + ", c = " + c + ";");
```

The output is

Here it is: a = 11, b = 13, c = 48

To summarize the sequence of events for a string context:

+   1. An empty buffer is constructed.
2. Each argument in turn is concatenated to the string buffer, using the append() method.
3. The string buffer is converted to a string by a call to toString().

That is all you need to know about string manipulation for the Certification Exam, and it’s probably all you need to know to write effective and efficient code, too.