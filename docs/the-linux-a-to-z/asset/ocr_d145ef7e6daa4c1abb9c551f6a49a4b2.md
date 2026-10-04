```
END_IF
```

# Switch context to the remembered ‘highest counter’ process

As you can see, this is a very simple scheduling algorithm that depends largely on the counter value to determine how likely a process is to run and, when it does run, the size of its time slice.

In kernels which can support multiple processors there is a simple modification to the way in which the counter value is used to select the next process to run. Instead of just using the counter on its own, there are extra terms added to give some advantage to processes on the same processor and also to give a small advantage to the current process.

With these notes and a copy of your Linux kernel scheduler source code to hand, it should be fairly easy for you to run through the code and sort out how it works.