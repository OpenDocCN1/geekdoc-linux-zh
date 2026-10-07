
classes Member (representing a person who is a member of the library) and Book (representing a single copy of a book):

+   1. private Book reserveACopy(String title, Member member) {
2. assert isValidTitle(title);
3.
4. Book book = getAvailableCopy(title);
5. reserve(book, member);
6.
7. assert isInStock(book);
8. return book;
9. }

Line 2 enforces a precondition. If the title is not valid (perhaps someone accidentally typed "Moby-Duct"), then the method should terminate as soon as possible, before any damage can be done. In fact, if the precondition fails, the failure indicates that the class needs more work. The code that called reserveACopy() with bad arguments needs to be fixed. The assertion failed (we hope) during in-house testing. Eventually the Library class would be debugged so that reserveACopy() would never be called with bad arguments. When the author is satisfied (and not before this point), the class would be ready for the field, where assertions would be disabled.

Line 7 enforces a postcondition. The body of the method is supposed to find an available copy of the desired book. If the book was found not available after all, then a problem exists with the method's algorithm. The method should be terminated immediately before the library's data gets hopelessly corrupted, and the method should be debugged. When the author of the method has failed the algorithm's correctness, the method can be shifted to an environment where assertions can be disabled.

There is a subtle point to be made about the appropriateness of assertions to check preconditions of public methods. Note that the method in our example was private, so it could be called only from within our class. Thus if the assertion on line 2 failed, you could point the finger of blame upon yourself or at a colleague; nobody else could call reserveACopy(). However, if the method were public, it could be called by anyone, including a customer who bought the class for a separate product. Such a programmer is beyond your control of quality assurance. A call to reserveACopy() with bad arguments would not necessarily indicate an internal problem within the Library class. If the reserveACopy() method were public, preconditions would have to be checked without the assertion mechanism, because the bad call would have failed in the field with assertions disabled.

The following code shows how to use an exception to indicate precondition failure:

+   1. public Book reserveACopy(String title, Member member) {
2. if (!isValidTitle(title))
3. throw new IllegalArgumentException("Bad title: " + title);
4.
5. Book book = getAvailableCopy(title);
6. reserve(book, member);
7.
8. assert bookIsInStock(book);
9. return book;
10. }

IllegalArgumentException is a runtime exception, so reserveACopy() does not need a throws clause and callers do not need to use the try/catch mechanism.

The previous example demonstrates that assertions are not appropriate for checking preconditions in public methods.

![](img/09f8389b7ae2705d1ab14be2d5e857e3_187_0.png)

# Practicing with Assertions

In this exercise, you will modify a very simple class to take advantage of assertions. The original code, which appears in the AssertCheckStarting.java file on the CD-ROM, is as follows:

```java
public class AssertCheckStarting {
    private final static int SUIT_CLUBS = 0;
    private final static int SUIT_DIAMONDS = 1;
    private final static int SUIT_HEARTS = 2;
    private final static int SUIT_SPADES = 3;

    private final String[] suitNames = {
        "Clubs", "Diamonds", "Hearts", "Spades"
    };

    private final String suitToName(int suitNum) {
        return suitNames[suitNum];
    }

    public static void explainSuitNum(int suitNum) {
        System.out.println("Suit #" + suitNum + " is " + suitToName(suitNum));
    }

    public static void main(String[] args)
    {
        int suitNum = Integer.parseInt(args[0]);
        explainSuitTo(suitNum);
    }
}
```

The explainSuitTo() method is public, presumably so that it can be called from other classes; it calls suitToName(), which is appropriately private, since it has knowledge of how the class internally represents suit name.

Your assignment is to modify suitToName(), explainSuitToName(), or both, so that they appropriately check their preconditions. One possible solution appears in the file AssertCheckFinal.java on the CD-ROM. The method comments explain the solution.

# Summary

This chapter covered various aspects of flow control in Java. It began by discussing Java's three loop constructions: while(), do, and for(). These can be used with traditional syntax, but Java has expanded this by adding labeled break and continue statements, as well as the enhanced-for syntax.

We then covered Java's two selection constructs: the if()/else and switch() statements which provide ways to conditionally execute code.

The chapter ended with a discussion of exceptions and assertions. Exceptions indicate abnormal termination of try blocks or methods, and must be dealt with programmatically. Assertions indicate bugs.

# Exam Essentials

Understand the operation of Java while, do, and for loops. Understand labeled loops, labeled breaks, and labeled continues in these loops. You should be able to construct each kind of loop and know when loops are executed and conditions are evaluated. Know how flow control proceeds in each of them. Understand the syntax of the enhanced-for loop. Know the syntax of if/else and switch() statements. Understand the difference between checked and runtime exceptions. Understand how to use assertions to find bugs.

# Review Questions

+   1. Consider the following code:

```java
for (int i = 0; i < 2; i++) {
  for (int j = 0; j < 3; j++) {
    if (i == j) {
      continue;
    }
    System.out.println("i = " + i + " j = " + j);
  }
}
```

Which lines would be part of the output? (Choose all apply.)

A. i = 0 j = 0
B. i = 0 j = 1
C. i = 0 j = 2
D. i = 1 j = 0
E. i = 1 j = 1
F. i = 1 j = 2

+   2. Consider the following code:

Which lines would be part of the output? (Choose all apply.)

A. i = 0 j = 0
B. i = 0 j = 1
C. i = 0 j = 2
D. i = 1 j = 0
E. i = 1 j = 1
F. i = 1 j = 2

+   3. Which of the following are legal loop constructions? (Choose all apply).

A. while (int i < 7) {
  i++;
  System.out.println("is is " + i);
}

B. int i = 3;
while (i) {
  System.out.println("is is " + i);
}

C. for (int k=0, j != 10; j++,k++) {
  System.out.println("j*" + j + ", k=* " + k);
}

D. int j=0;
do {
  System.out.println("j*" + j++);
  if (j==3) {
    continue loop;
  }
} while (j<10);

+   4. What would be the output from this code fragment?

```java
int x = 0, y = 4, z = 5;

if (x > 2) {
  if (y < 5) {
    System.out.println("message one");
  }
} else {
  System.out.println("message two");
} else if (z > 5) {
  System.out.println("message three");
} else {
  System.out.println("message four");
}
```

A. message one
B. message two
C. message three
D. message four
