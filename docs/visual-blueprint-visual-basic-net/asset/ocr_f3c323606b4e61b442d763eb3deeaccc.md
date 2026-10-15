# Extra

Keeping track of a large number of threads consumes significant processor time. If you need to use a large number of threads, for example ten or twenty, you may find that they perform very poorly because the system spends more time switching between threads than running them. Also, if you are using most of the processor time in your process, threads in other processes run less frequently. You can ease the requirements of threading by using the minimum number of threads to accomplish a particular task. For example, you may need to search four different database tables or download ten different Web pages in your application. You know threads enable your application to respond to the user during this operation, but creating all the threads at once for the operation can cause more harm than good, especially on slower computers. Experiment with different numbers of concurrent threads to see which yields the best performance. See the section “Write Thread-Safe Code” to learn how you can start a new thread when one completes using the Join method or a ThreadPool object. Threadpool allows you to queue an unlimited number of threads and let the system determine how many to run.

![](bbox=[0.07, 0.49, 0.48, 0.82])

![](bbox=[0.52, 0.49, 0.93, 0.82])

6 On a new line, type the variable name for the thread followed by .Start()

7 Repeat steps 3 through 7 to start as many threads as necessary.

B Press F5 to run your project.

The threads run the code in the method concurrently.

> Note: To write thread-safe code for multiple threads or for input and output operations, see the section "Write Thread-Safe Code."