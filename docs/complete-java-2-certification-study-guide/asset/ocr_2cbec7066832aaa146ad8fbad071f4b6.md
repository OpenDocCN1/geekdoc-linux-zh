4. continue mainLoop;

5. }

6. }

7. )

Notice particularly the label mainLoop that has been applied to the for() on line 1. The fact that this is a label is indicated by the trailing colon: You typically apply labels of this form to the opening loop statements: while(), do, or for.

Here, when the processing of the second array comes across a 0 value, it abandons the whole processing not just for the inner loop but for the current object in the array. This is equivalent to jumping to the statement i++ in the first for() statement.

You might still think this is not any advantage over using if() statements, but imagine that further processing was done between lines 6 and 7, and finding the 0 character in the array was required to avoid that further processing. To achieve that without using continue, you would have to set a flag in the inner loop and use it to abandon the outer processing. It can be done, but it is rather messy.

# Using break

The break statement, when applied to a loop, is somewhat like the continue statement. However, instead of prematurely completing the current iteration of a loop, break causes the entire loop to be broken. Consider this example:

+   1. for (int j = 0; j < array.length; j++) {
2. if (array[j] == null) {
3. break; //break out of inner loop
4. }
5. // process array[j]
6. )

In this case, instead of simply skipping processing for array[j] and proceeding directly to processing array[j+1], this version quits the inner loop as soon as a null element is found. You can also use on break statements, and as before, you must place a matching label on one of the enclosing blocks. The break and continue statements provide a convenient way to make parts of a loop conditional, especially when used in their labeled formats.

The next section discusses the if()/else and switch() constructions, which provide the normal means of implementing conditional code.

# The Selection Statements

Java provides a choice of two select constructs: the if()/else and switch() mechanisms You can easily write simple conditional for a choice of two execution paths based on the value of a boolean expression if()/else. If you need more complex choices between