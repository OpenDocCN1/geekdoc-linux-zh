
## Extra

Keeping track of a large number of threads consumes significant processor time. If you need to use a large number of threads, for example ten or twenty, you may find that they perform very poorly because the system spends more time switching between threads than running them. Also, if you are using most of the processor time in your process, threads in other processes run less frequently. You can ease the requirements of threading by using the minimum number of threads to accomplish a particular task. For example, you may need to search four different database tables or download ten different Web pages in your application. You know threads enable your application to respond to the user during this operation, but creating all the threads at once for the operation can cause more harm than good, especially on slower computers. Experiment with different numbers of concurrent threads to see which yields the best performance. See the section “Write Thread-Safe Code” to learn how you can start a new thread when one completes using the Join method or a ThreadPool object. ThreadPool allows you to queue an unlimited number of threads and let the system determine how many to run.

![](img/d6f772854306e15fb6df39b861a7b541_212_0.png)

![](img/d6f772854306e15fb6df39b861a7b541_212_1.png)

6. On a new line, type the variable name for the thread followed by `.Start()`.
7. Repeat steps 3 through 6 to start as many threads as necessary.
8. Press F5 to run your project.

The threads run the code in the method concurrently.

> Note: To write thread-safe code for multiple threads or for input and output operations, see the section "Write Thread-Safe Code."

## Write Thread-Safe Code

Although threading is one of the most difficult and frustrating tasks in modern programming, Visual Basic .NET makes threading simple and easy when you carefully program. The problem with free-threading is that every thread of your application runs in the same memory space, meaning the threads all access the same objects. You must make sure that the threads of your application do not interfere with each other by interacting with the same object. You can use commands in VB .NET to create thread-safe code.

In general, the .NET Framework is not thread-safe, meaning if two threads attempt to access the same object at the same time, the object does not contain code to respond properly. Particularly, the Windows Forms classes cause many problems when not carefully managed.

To make sure you do not have more than one thread access an object, you use the SyncLock block. When you use the SyncLock statement, you provide VB .NET with an object, inside parentheses, on which to lock. The `End SyncLock` statement marks the end of the block you want to lock. For example, you may have a list of results that you want to load into a ListBox control. However, you do not want more than one thread to access the ListBox at once, because the ListBox control is not thread-safe. You can provide the ListBox control as the SyncLock object and place the command to add information to the ListBox inside the lock. Then, if another thread runs the same lines of code, VB .NET forces the thread to wait until the previous lock releases.

In some cases, you can start a thread after another completes to avoid synchronizing objects in use by the two threads. Call the Join() method and pass another thread object as the parameter to cause the thread to wait until the thread you specify completes. Place this command inside the code of another thread to make it wait for another thread to complete.

![](img/d6f772854306e15fb6df39b861a7b541_213_0.png)

![](img/d6f772854306e15fb6df39b861a7b541_213_1.png)

1. Open a module that contains the method the thread runs.
2. Type `SyncLock()`.
3. Inside the parentheses, type the object on which you want VB .NET to lock.
4. Press Enter to complete the block statement.
   - VB .NET creates the `End SyncLock` statement.

> Note: For more information about creating a thread, see the section “Create a Thread.”
