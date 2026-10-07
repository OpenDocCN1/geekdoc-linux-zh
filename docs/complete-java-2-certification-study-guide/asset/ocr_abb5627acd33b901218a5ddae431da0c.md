5. Which statement is true about the following code fragment?

```
1. int j = 2;
2. switch (j) {
3. case 2:
4. System.out.println("value is two");
5. case 2 + 1:
6. System.out.println("value is three");
7. break;
8. default:
9. System.out.println("value is " + j);
10. break;
11. }
```

A. The code is illegal because of the expression at line j, as the argument to the switch() construct, can be any of byte, short, int, or long.

B. The output would be the text value two.

C. The output would be the text value two followed by the text value three.

D. The output would be the text value two, followed by the text value is three, followed by the text value is 2.

6. Consider the following class hierarchy and code fragment:

```
java.lang.Exception
java.io.IOException
/ \\
java.io.StreamCorruptedException java.net.MalformedURLException
```

```
1. try {
2. // assume s is previously defined
3. URL u = new URL(s);
4. // in is an ObjectInputStream
5. Object o = in.readObject();
6. System.out.println("Success");
7. }
8. catch (MalformedURLException e) {
9. System.out.println("Bad URL");
10. }
11. catch (StreamCorruptedException e) {
12. System.out.println("Bad file contents");
13. }
14. catch (Exception e) {
15. System.out.println("General exception");
16. }
```