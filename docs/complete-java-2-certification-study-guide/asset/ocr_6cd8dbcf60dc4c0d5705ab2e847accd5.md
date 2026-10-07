}

```
public PhaserBankException(Throwable cause) {
  super(cause);
}
```

```
public PhaserBankException(String message, Throwable cause) {
  super(message);
}
```

Custom exception types are always the right choice when the core classes don’t contain an exception whose name describes your situation.

# Exceptions and Overriding

When you extend a class and override a method, the Java compiler insists that all exception **classes thrown by the new method must be the same as, or subclasses of, the exception classes thrown by the original method.** Consider these examples (assume they are declared in separate source files; the line numbers are simply for reference):

+   1. public class BaseClass {
2. public void method() throws IOException {
3. }
4. }
5.
6. public class LegalOne extends BaseClass {
7. public void method() throws IOException {
8. }
9. }
10.
11. public class LegalTwo extends BaseClass {
12. public void method() {
13. }
14. }
15.
16. public class LegalThree extends BaseClass {
17. public void method()
18. throws EOFException, MalformedURLException {
19. }
20. }
21.