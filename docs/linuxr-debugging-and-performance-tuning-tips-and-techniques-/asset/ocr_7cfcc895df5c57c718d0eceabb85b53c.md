The calculation on line 39 of $j$, the array element count, uses a lovely, portable trick: The number of elements is the size of the entire array divided by the size of the first element. The beauty of this idiom is that it's always right: No matter how many elements you add to or remove from such an array, the compiler will figure it out. It also doesn't require a terminating *sentinel* element; that is, one in which all the fields are set to zero, NULL, or some such.

The work is done by a loop (lines 41-55), which seeks to the byte offset given in each structure (line 42) and then writes the structure out (line 49):

```
41       for (i = 0; i < j; i++) {
42             if (lseek(fd, people[i].pos, SEEK_SET) < 0) {
43                 fprintf(stderr, "%s: %s: seek error: %s\n",
44                       argv[0], argv[1], strerror(errno));
45                 (void) close(fd);
46                 return 1;
47             }
48         }
49         if (write(fd, &people[i], sizeof(people[i])) != sizeof(people[i])) {
50             fprintf(stderr, "%s: %s: write error: %s\n",
51                     argv[0], argv[1], strerror(errno));
52             (void) close(fd);
53             return 1;
54         }
55         }
56     }
57
58     /* all ok here */
59     (void) close(fd);
60     return 0;
61     }
```

Here are the results when the program is run:

```
$ ch04-holes peopelost       *Run the program*
$ ls -ls peopelost           *Show size and blocks used*
  16  -rw-r--r--  1 arnold devel    81,944 Mar 23 17:43 peopelost
$ echo 81944 / 4096 | bc -l  *Show blocks if no holes*
20.0058593750000000000
```

We happen to know that each disk block in the file uses 4096 bytes. (How we know that is discussed in Section 5.4.2, “Retrieving File Information,” page 141. For now, take it as a given.) The final `bc` command indicates that a file of size 81,944 bytes needs 21 disk blocks. However, the `-ls` option to `ls`, which tells us how many blocks a file