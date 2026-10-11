Now, assume that there are two threads of execution, both enter this critical region, and the initial value of i is 7. The desired outcome is then similar to the following (with each row representing a unit of time):

| Thread 1 | Thread 2 |
| :------- | :------- |
| get i (7) | — |
| increment i (7→8) | — |
| write back i (8) | — |
| — | get i (8) |
| — | increment i (8→9) |
| — | write back i (9) |

As expected, 7 incremented twice is 9. A possible outcome, however, is the following:

| Thread 1 | Thread 2 |
| :------- | :------- |
| get i (7) | get i (7) |
| increment i (7→8) | — |
| — | increment i (7→8) |
| write back i (8) | — |
| — | write back i (8) |

If both threads of execution read the initial value of i before it is incremented, both threads increment and save the same value. As a result, the variable i contains the value 8 when, in fact, it should now contain 9. This is one of the simplest examples of a critical region. Thankfully, the solution is equally as simple: We merely need a way to perform these operations in one indivisible step. Most processors provide an instruction to atomically read, increment, and write back a single variable. Using this *atomic instruction*, the only possible outcome is

| Thread 1 | Thread 2 |
| :------- | :------- |
| increment & store i (7→8) | — |
| — | increment & store i (8→9) |

Or conversely

| Thread 1 | Thread 2 |
| :------- | :------- |
| — | increment & store (7→8) |
| increment & store (8→9) | — |