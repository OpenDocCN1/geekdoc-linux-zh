
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
/ \
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
17. finally {
18. System.out.println("Doing finally part");
19. }
20. System.out.println("Carrying on");
```

What lines are output if the constructor at line 3 throws a MalformedURLException? (Choose all that apply.)

- A. Success
- B. Bad URL
- C. Bad file contents
- D. General exception
- E. Doing finally part
- F. Carrying on

7. Consider the following class hierarchy and code fragment:

```
java.lang.Exception
java.io.IOException
java.io.StreamCorruptedException
java.net.MalformedURLException
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
17. finally {
18. System.out.println("Doing finally part");
19. }
20. System.out.println("Carrying on");

What lines are output if the methods at lines 3 and 5 complete successfully without throwing any exceptions? (Choose all that apply.)

- A. Success
- B. Bad URL
- C. Bad file contents
- D. General exception
- E. Doing finally part
- F. Carrying on

8. Consider the following class hierarchy and code fragment:

```
java.lang.Throwable
  / \
  /     \
java.lang.Error      java.lang.Exception
java.lang.OutOfMemoryError      java.io.IOException
java.io.StreamCorruptedException      java.net.MalformedURLException
```

```
1. try {
2.   // assume s is previously defined
3.   URL u = new URL(s);
4.   // in is an ObjectInputStream
5.   Object o = in.readObject();
6.   System.out.println("Success");
7. }
8. catch (MalformedURLException e) {
9.   System.out.println("Bad URL");
10. }
11. catch (StreamCorruptedException e) {
12.  System.out.println("Bad file contents");
13. }
14. catch (Exception e) {
15.  System.out.println("General exception");
16. }
17. finally {
18.  System.out.println("Doing finally part");
19. }
20. System.out.println("Carrying on");
```

What lines are output if the method at line 5 throws an OutOfMemoryError? (Choose all that apply.)

- A. Success
- B. Bad URL
- C. Bad file contents
- D. General exception
- E. Doing finally part
- F. Carrying on

9. Which of the following are appropriate situations for assertions?
A. Preconditions of a public method
B. Postconditions of a public method
C. Preconditions of a private method
D. Postconditions of a private method

10. Consider the code:
1. public class Assertification {
2. public static void main(String[] args) {
3. args.length == 0;
4. }

Which of the following conditions must be true in order for the code to throw an AssertionError? Assume you are release 5.0. (Choose all that apply.)

- A. The source code must be compiled with -source1.5 flag.
- B. The application must be run with -enableassertions flag or another assertion-enabling flag.
- C. The args array must have zero elements.
- D. The args array must have one or more elements.

11. Which of the following is the most appropriate way to handle invalid arguments in a public method?
A. Throw java.lang.InvalidArgumentException.
B. Throw java.lang.IllegalArgumentException.
C. Check for argument validity in an assert statement, which throws AssertionError when the arguments are invalid.
D. Use non-assert code to check for argument validity. If invalid arguments are detected, explicitly throw AssertionError.

## 5 Flow Control, Assertions, and Exception Handling

12. Suppose salaries is an array containing floats. Which of the following are valid loop statements for processing each element of salaries?

- A. for (float i : salaries)
- B. for (int i : salaries)
- C. for (float f : salaries)
- D. for (int i : salaries)

13. Which of the following are legal? (Choose all apply.)

- A. for (int i=0, j=1; i<10; i++, j++)
- B. for (int i=0, j=1; i<10; i++, j++)
- C. for (int i=0, float j=1; i++, j++)
- D. for (String s = ""; s.length()<10; s += "")

14. A method called finallyTest() consists of a try block, followed by a catch block, followed by a finally block. Assuming the JVM doesn't crash and the code does not execute System.exit(), under what circumstances will the finally block not execute?

- A. The try block throws an exception, and the catch block also throws an exception.
- B. The try block throws an exception, that is not handled by the catch block.
- C. The try block throws an exception, and the catch block calls finallyTest() in a way that causes another exception to be thrown.
- D. If the JVM doesn't crash and the code does not execute System.exit(), the finally block will always execute.

15. Which of the following are loop definitions? (Choose all that apply.)

- A. while (int a = 0) { /* whatever */ }
- B. while (int a == 0) { /* whatever */ }
- C. do { /* whatever */ } while (int a = 0)
- D. do { /* whatever */ } while (int a == 0)
- E. for (int a=0; a<100; a++) { /* whatever */ }
- F. None of them.

16. Which of the following are legal argument types for a switch statement?

- A. byte
- B. int
- C. long
- D. float
- E. char
- F. String

## Review Questions

17. When is it appropriate to pass a cause to an exception's constructor?
A. Always
B. When the exception is thrown in response to catching a different type
C. When the exception is thrown from a public method
D. When the exception is thrown from a private method

18. Which of the following should always be caught?
A. Runtime exceptions
B. Checked exceptions
C. Assertion errors
D. Errors other than assertion

19. When does an exception's stack trace get recorded in the exception object?
A. When the exception is constructed
B. When the exception is thrown
C. When the exception is caught
D. When the exception's printStackTrace() method is called

20. When is it appropriate to write code that constructs and throws an error?
A. When a public method's preconditions are violated
B. When a public method's postconditions are violated
C. When a nonpublic method's preconditions are violated
D. When a nonpublic method's postconditions are violated
E. Never

## Answers to Review Questions

1. B, C, D, F. The loops iterate from 0 to 1 and j from 0 to 2. However, the inner loop executes a continue statement when the values of i and j are the same. The output is generated inside the inner loop, after the continue statement, no output is generated when the values are the same. Therefore, the outputs suggested by options A and E are skipped.

2. D. It seems the variable i will take the values 0 and 1, and for each of these values, j will take values 0, 1, and 2. However, whenever i and j have the same value, the outer loop is continued before the output is generated. Because the outer loop is target of the continue statement, the statement of the inner loop is abandoned. Therefore, only the line to be output is shown in option D.

3. In A, the declaration for i is illegal. This type of declaration is permitted only in the first part of a for() loop. In B, the outer loop expression—the variable in this case—is of int. A boolean expression is required. C is valid. Despite the complexity of declaring one value inside the for() construction and outside (along with the use of the comma operator in the end part), this is entirely legitimate. D would be correct, if the label omitted from the second line, which should read loop: {

4. D. The first test at line 2 fails, which immediately cuts control to skip to line 10, bypassing both tests that might result in the output of one message or two. So, even though the test at line 3 would be true, it is never made; A is not. At line 10, the output is false, so the message at line 1 is skipped, but message, at line 14, is output.

5. D is incorrect because the code does the expression at line 5: the expression is a constant. B is incorrect because the switch can take a long argument. Only short, char and int are acceptable. The output results from the value 2 like this, the option case 2 is selected, which output is two. However, there is no break statement between lines 4 and 5, so the execution enters the next case and outputs 13 from line 6. The default: part of a switch() is executed only when no options have been selected, or if no break precedes. Neither of these situations holds, so the output consists only the two messages listed in D.
