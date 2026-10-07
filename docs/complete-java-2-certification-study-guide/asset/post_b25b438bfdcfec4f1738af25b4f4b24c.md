
13. Which of the following are legal import statements?

-   A. import java.util.Vector;
-   B. static import java.util.Vector.*;
-   C. import static java.util.Vector.*;
-   D. import java.util.Vector static;

14. Which of the following may be statically imported? (Choose all that apply).

-   A. Package names
-   B. Static method names
-   C. Static field names
-   D. Method-local variable names

15. What happens when you try to compile and run the following code?

```
public class Q15 {
    static String s;
    public static void main(String[] args) {
        System.out.println(">>>" + s + "<<");
    }
}
```

-   A. The code does not compile
-   B. The code compiles, and prints out >>null<<
-   C. The code compiles, and prints out >>null<<

16. Which of the following are legal? (Choose all that apply).

-   A. int a = abcd;
-   B. int b = ABCD;
-   C. int c = 0abcd;
-   D. int d = 0ABCD;
-   E. int e = 0abcd;
-   F. int f = 0ABCD;

17. Which of the following are legal? (Choose all that apply).

-   A. double d = 1.2d;
-   B. double d = 1.2D;
-   C. double d = 1.2d5;
-   D. double d = 1.2D5;

## Review Questions 33

18. Which of the following are legal?
A. char c = \u1234;
B. char c = \u1234;
C. char c = '\u1234';

19. Consider the following code:
1. StringBuilder sbuf = new StringBuffer();
2. sbuf = null;
3. System.gc();

Choose all true statements:
A. After line 2 executes, the StringBuilder object is garbage collected.
B. After line 3 executes, the StringBuilder object is garbage collected.
C. After line 2 executes, the StringBuilder object is eligible for garbage collection.
D. After line 3 executes, the StringBuilder object is eligible for garbage collection.

20. Which of the following are true? (Choose all that apply)
A. Primitives are passed by reference.
B. Primitives are passed by value.
C. References are passed by reference.
D. References are passed by value.

## Answers to Review Questions

- 1. The range of negative numbers is greater than the range of positive numbers.

- 2. A, B, C, D, E. All of the identifiers are defined with a letter, a dollar sign, or an underscore; subsequent characters may be letters, dollar signs, underscores, or digits. And of course keywords and their kin may not be identifiers.

- 3. B, D. All the choices are valid method signatures. However, in order to be the entry point of an application, a `main()` method must be public, static, and void; it must take a single argument of type `String[]`.

- 4. Package declaration must come first, followed by imports, followed by class/interface/enum definitions.

- 5. A, E. The array has 25 elements, indexed from 0 through 24. All elements are initialized to 0.

- 6. D is constructed on line 3. A reference to that holder is passed into method `bump()` on line 5. Within the method call, the holder's variable is bumped from 100 to 101.

- 7. The `decrement()` method is passed as a copy of the argument d; the copy gets decremented, but the original is untouched

- 8. Garbage collection cannot be forced. Calling `System.gc()` or `Runtime.gc()` is not 100 percent reliable, because the garbage-collection thread might defer to a thread of higher priority; thus options B and D are incorrect. Option C is correct because the two `gc()` methods do not take arguments; if you still have a reference to pass into any method, the object is not eligible to be collected. Option E will make the object eligible for collection the next time the garbage collector runs.

- 9. The range for a 16-bit short is $-2^{15}$ through $2^{15}-1$. This range is part of the Java specification, regardless of the underlying hardware.

- 10. The range for an 8-bit byte is $-2^{7}$ through $2^{7}-1$. Table 1.3 lists the ranges for Java's integral primitive types.

- 11. Importing increases compilation time.

- 12. A., Importing is strictly a compile-time function. It has no effect on class loading or on any other run-time function.

- 13. A, C. The `import` keyword may optionally be followed by the `static` keyword.

- 14. B, C. You may statically import method and field names.

- 15. C. The code compiles without error. At static initialization, `s` is initialized to null (and not to an empty string, as suggested by C).

- 16. C, D. The characters a–f and A–F may be combined with the digits 0–9 to form a hexadecimal literal, which must begin with 0x.

- 17. A, B. The d suffix in option A and the D suffix in option B are optional. Options C and D are illegal because the notation requires e or E, not d or D.

- 18. C. A Unicode literal character must be enclosed in single quotes and must begin with \u.

- 19. C. After line 2 executes, there are no references to the StringBuffer object, so it becomes eligible for garbage collection.

- 20. B, D. In Java, all arguments are passed by value.

## Chapter 2

## Operators and Assignments

JAVA CERTIFICATION EXAM OBJECTIVES COVERED IN THIS CHAPTER:

- 7.6 Write code that correctly applies the appropriate operators including assignment operators (limited to: =, +=, -=), arithmetic operators (limited to: +, -, *, /, %, ++, --), relational operators (limited to: <, <=, >=, !=), the instanceof operator, logical operators (limited to: &&, ||), and the conditional operator.

## Overview of Operators

Java provides a full set of operators, which are shown in Table 2.1, perform arithmetic and logical operations. Before we start, let's look at the general issue of operators.

| Category | Operators |
| :--- | :--- |
| Unary | ++ - ! ~ (type |
| Arithmetic | * / % + - |
| Shift | << >> >>> |
| Comparison | < <= >= instanceof == !== |

| Category | Operators |
| :--- | :--- |
| Bitwise | & ^ |
| Short-circuit | && || |
| Conditional | ?: |
| Assignment | = op= |

## Order

In Java, the order of evaluation of operands in an expression is fixed. Consider this code fragment:

1. int [] a = { 4, 4 };
2. int b = 1;
3. a[b] = b = 0;

In this case, it might be unclear which element of the array is modified: Which of b is to select the array element, 0 or 1? Evaluation from left to right requires that the leftmost expression, a[b], be evaluated, so it is a reference to the variable b. The constant expression 0 is evaluated next, which does not involve any work. Now that the operands have been evaluated, the operations take place. This is done in the order specified by precedence and associativity. For assignments, associativity is right to left, so the value 0 is first assigned to the variable b; then the value 0 is assigned into the last element of the array a.

Although Table 2.1 shows the precedence order, the degree of detail in this precedence ordering is rather high. It is generally better style to keep expressions simple and use redundant bracketing to make clear how any particular expression should be evaluated. This approach reduces the chance that less-experienced programmers will have difficulty trying to read or maintain your code. Bear in mind that the code generated by the compiler will be the same despite redundant brackets.
