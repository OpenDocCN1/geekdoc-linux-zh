```
* wake_up(&WaitQ) (only module_close does that,
* when the file is closed) or when a signal, such
* as Ctrl-C, is sent to the process */
module_interruptible_sleep_on(&WaitQ);
```

```
/* If we woke up because we got a signal we're not
* blocking, return -EEINTR (fail the system call),
* This allows processes to be killed or stopped. */
```

```
/*
* Emmanuel Papirakis:
*
* This is a little update to work with 2.2*. Signals
* are now contained in two words (64 bits) and are
* stored in a structure that contains an array of two
* unsigned longs. We have to make 2 checks in our if.
*
* Ori Pomerantz:
*
* Nobody promised they'll never use more than 64
* bits, or that this book won't be used for a version
* of Linux with a word size of 16 bits. This code
* would work in any case.
/
```

```
#if LINUX_VERSION_CODE >= KERNEL_VERSION(2,2,0)

for(i=0;i<NSIG_WORDS && !is_sig; i++)
    is_sig = current->signal.sig[i] &
      current->blocked.sig[i];
if (is_sig) {
#else
    if (current->signal & current->blocked) {
#endif
    /* It's important to put MOD_DEC_USE_COUNT here,
```