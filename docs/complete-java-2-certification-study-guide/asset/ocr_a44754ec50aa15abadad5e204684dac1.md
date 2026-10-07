7. Which of the following statements are true? (Select all that apply.)

+   A. A final object's data cannot be changed.
B. A final class can be subclassed.
C. A final method cannot be overloaded.
D. A final object cannot be reassigned a new address in memory.
E. None of the above.

8. The keyword extends refers to what type of relationship?

+   A. "is a"
B. "has a"
C. "was a"
D. "will be a"
E. None of the above

9. Which of the following keywords is used to invoke a method in the parent class?

+   A. this
B. super
C. final
D. static

10. Given the following code, what will be the outcome?

```
public class Funcs extends java.lang.Math {
    public int add(int x, int y) {
        return x + y;
    }
    public int sub(int x, int y) {
        return x - y;
    }
    public static void main(String [] a) {
        Funcs f = new Funcs();
        System.out.println("**" + f.add(1, 2));
    }
}
```

+   A. The code compiles but does not output anything.
B. "3" is printed out to the console.
C. The code does not compile.
D. None of the above.