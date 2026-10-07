+   7. Consider the following class definition:
1. public class Test extends Base {
2. public Test(int j) {
3.   }
4. public Test(int j, int k) {
5.   super(j, k);
6.   }
7. )

Which of the following forms of constructor must exist explicitly in the definition of the Base class? Assume Test and Base are in the same package. (Choose all that apply.)

+   A. Base() { }
B. Base(int j) { }
C. Base(int j, int k) { }
D. Base(int j, int k, int l) { }

+   8. Consider the following class definition:
1. public class Outer {
2. private int a = 1;
3. private int b = 2;
4. private void method(final int c) {
5.   int d = 3;
6.   class Inner {
7.     private void iMethod(int e) {
8.     }
9.   }
10. }
11. }

Which variables can be referenced at line 8? (Choose all that apply).

+   A. a
B. b
C. c
D. d
E. e