# ## Events, Signals, and Callbacks

This chapter deals with some of the problems that arise from using the event model. If the program constantly remains blocked waiting for input from the event queue, there is no opportunity to read data from files or over a communication link. Another problem comes from the fact that whenever your program is processing data, it is ignoring the event queue and it also ignores any mouse and keyboard input.

Events come in through the event queue, they are translated into signals, and the signals cause callback functions to be called. But because there are so many signals defined in so many different places in the code, it can become very confusing for a programmer trying to keep track of them. And it is hard to keep track of which arguments are being passed to which callback functions.

# ## Reading the Event Queue

The _event queue_ is the center of every application. Not only does the event queue supply the information from the user’s mouse and keyboard, it also can be used as a timer and as a method of inter-process communications.

Your application initializes itself and then calls the function `gtk_main()`, which does not return until it is time for your process to halt. You can verify this by surrounding the call to `gtk_main()` with two print statements like this:

```
```
g_print("The call to gtk_main()\n");
gtk_main();
g_print("The return from gtk_main()\n");
```
```

When the program is run, the first line displays immediately (well, as soon as the program finishes initializing itself and is

# ### In This Chapter

+   - Receiving and using events sent to your program from the mouse and the keyboard

+   - Understanding the origin of events, and the path they take to get to your program

+   - Learning how the events are named and numbered so you can know what your program should expect

+   - Issuing your own custom event messages so they appear in the input queue

+   - Using the input event queue as a way to implement timers and background processing