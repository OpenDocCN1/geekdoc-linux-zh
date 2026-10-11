Much old code uses the numeric values shown in Table 4.4. However, any new code you write should use the symbolic values, whose meanings are clearer.

The meaning of the values and their effects upon file position are shown in Figure 4.1. Assuming that the file has 3000 bytes and that the current offset is 2000 before each call to lseek(), the new position after each call is as shown:

![](bbox=[0.08, 0.28, 0.92, 0.48])

# FIGURE 4.1
Offsets for lseek()

Negative offsets relative to the beginning of the file are meaningless; they fail with an “invalid argument” error.

The return value is the new position in the file. Thus, to find out where in the file you are, use

```
```
off_t curpos;
...
curpos = lseek(fd, (off_t) 0, SEEK_CUR);
```
```

The 1 in lseek() stands for long. lseek() was introduced in V7 Unix when file sizes were extended; V6 had a simple seek() system call. As a result, much old documentation (and code) treats the offset parameter as if it had type long, and instead of a cast to off_t, it’s not unusual to see an L suffix on constant offset values:

```
```
curpos = lseek(fd, 0L, SEEK_CUR);
```
```

On systems with a Standard C compiler, where lseek() is declared with a prototype, such old code continues to work since the compiler automatically promotes the 0L from long to off_t if they are different types.

One interesting and important aspect of lseek() is that it is possible to seek beyond the end of a file. Any data that are subsequently written at that point go into the file,