+   4. Which of the following statements is true?

+   A. Transient methods may not be overridden.
B. Transient methods must be overridden.
C. Transient classes may not be serialized.
D. Transient variables must be static.
E. Transient variables are not serialized.

+   5. Which statement is true about this application?

```
1. class StaticStuff
2. {
3. static int x = 10;
4.
5. static { x += 5; }
6.
7. public static void main(String args[])
8. {
9. System.out.println('x = ' + x);
10. }
11.
12. static { x /= 5; }
13. }
```

+   A. Lines 5 and 12 will not compile because the method names and return types are missing.
B. Line 12 will not compile because you can only have one static initializer.
C. The code compiles and execution produces the output x = 10.
D. The code compiles and execution produces the output x = 15.
E. The code compiles and execution produces the output x = 3.

+   6. Which statement is true about this code?

```
1. class HasStatic
2. {
3. private static int x = 100;
4.
5. public static void main(String args[])
6. {
7. HasStatic hs1 = new HasStatic();
8. hs1.x++;
9. HasStatic hs2 = new HasStatic();
10. hs2.x++;
```