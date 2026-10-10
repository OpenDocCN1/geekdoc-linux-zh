# Making P and V correct

The programmer's favorite approach is to make it the hardware designer's problem. We'll first look at how hardware can support implementations of semaphores and then how software alone can be used.

# Processor implementation

A number of systems provide instructions which automatically update a word in memory. These instructions not only cannot be interrupted, but they hold the bus so that another processor cannot modify the word.

For example, the Motorola MC68040 and the IBM 370 architectures offer a *test-and-set instruction* which reads a value from memory, compares it to zero (and sets a condition code) and sets it unconditionally to one. Our semaphore operations would now look like:

```
semaphore N = 0;  
void P(int *X) { while (test_and_set(*X) == 1) ; }  
void V(int *X) { *X = 0 ; }
```

Another common atomic read-modify-write instruction is the *swap instruction* found in the SPARC and the Motorola MC88100 processors. By swapping whatever is in memory with the value 1, one can mimic the test-and-set instruction above. (You'll note that because of the RISC architecture, the compiler will have to store the returned value and then explicitly test it.)

```
semaphore N = 0;  
void P(int *X) { while (swap(*X,1) == 1) ; }  
void V(int *X) { *X = 0 ; }
```

The DEC PDP-11 has *increment* and *decrement* instructions with atomic read-modify-write behavior. The condition code is set based on the value written. The following code has a counting semaphore which can also control the number of processes permitted to enter the critical section. The semaphore is merely set to the negative of the number of processes permitted in the critical section. A positive value represents the approximate number of processes waiting to enter the critical