```
```text
            snprintf(msg, sizeof(msg), "%ld getpid s", REPS);
            ec_negl( cl = clock() )
            gettimeofday(&tv1, NULL);
            timestart();
            for ( i = 0; i < REPS; i++)
                (void)getpid();
                (void)sleep(2);
            timestop(msg);
            gettimeofday(&tv2, NULL);
            ec_negl( c2 = clock() )
            printf("clock(): %.2f\n", (double)(c2 - cl) / CLOCKS_PER_SEC);
            printf("gettimeofday(): %.2f\n", TV_SUBTRACT(tv2, tv1));
            exit(EXIT_SUCCESS);

            EC_CLEANUP_BGN
                exit(EXIT_FAILURE);
            EC_CLEANUP_END
            }
```
```

This was the output on Linux (Solaris, FreeBSD, and Darwin gave similar results):

```
```text
1000000 getpids:
          "Total (user/sys/real)", 0.72, 0.44, 3.19
          "Child (user/sys)", 0.00, 0.00
clock(): 1.16
gettimeofday(): 3.19
```
```

So clock measured 1.16,26 exactly the sum of .72 and .44, and gettimeofday measured the same elapsed time as times. That’s good, or we would have more explaining to do.

If you want more resolution than times can give you, use getrusage instead (Section 5.16).

# 1.8 About the Example Code

There’s lots of example code in this book, and you’re free to use it for your own educational purposes or even in commercial products, as long as you give credit where you normally would, such as in an About dialog box or the credits page of a manual or book. For details, see the Web page www.basepath.com/amp/copyright.htm.

26. In the 1985 edition of this book, we got a time of 1.43 seconds for only 1000 getpids!