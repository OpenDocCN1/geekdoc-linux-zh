26. The goal is to create a regular expression that matches the run of digits in the middle of scanMe. The "d" in a regular expression indicates "digit". Two escaping backslashes are necessary: one for the Java compiler when it compiles the literal string. The second tells the useDelimiter() method that the "d" is a special character. The "*" matches zero or more occurrences; there are zero digits between the vowels, and is considered a "*" match, using \\d* splits into "a", "e", "i", etc.

27. The minus sign in the format string affects left-justification. The number to the right of the decimal point in format strings controls the number of digits to the right of the decimal point in the output.

28. A, D is correct the start() method of Thread (which is inherited by MyThread) causes a thread to begin execution of the thread's run() method. Calling run() directly as in B and C just the run() method to execute in the current thread. D creates a new thread whose target is one of MyRunnable; this is the typical way to run the Runnable interface.

29. A is correct the call to join() affects the thread, and the main thread will wait for the new thread to finish its execution before continuing any processing after the call to join().

30. A, B, D there are three locks to consider: the class lock, which controls the static methods, and the individual object locks, which control the non-static methods. A and B are true because staticMethod is controlled by the class lock. C is false because class1 not controlled by Class1's object, which is class1) staticMethod is controlled by the class lock. D is true because threads are trying to execute code controlled by Class1's object. E is false because thread A is executing code controlled by Class1's object, while B waits to execute code controlled by Class2's object.

31. C, E. The notify() and notifyAll() methods affect the threads that are waiting for the object on which the call is made. In other words, you notify the object, not so A and B don't work. When a thread is interrupted, it leaves the wait state and throws an InterruptedException, so C is correct. D does not work because there are multiple threads waiting for sharedObj. E works it guarantees that all waiting objects are moved out of the wait state.

32. Tightness of coupling expresses the degree to which one class relies on knowledge of the internals of another class. Tight coupling is undesirable if class stores data, class Driver (and any other similarly coupled classes) needs to be rewritten.

33. Cohesion is whether a class or method has its breaking down into smaller pieces; it is a desirable quality, chocolate and carrot cake can be broken down into two constituent parts, so it has inappropriate cohesion. This question does not concern coupling, which is an object's reliance on the internals of another entity's implementation

34. B, C, D. A cast is required when assigning from a superclass to a subclass, A requires a cast B does not. In the case C is required; the cast in D does not have harm. The cast in E turns the right-hand side of the assignment into an Object, which may not be assigned to a Citrus without a cast.