
## Finding Differences in Files with sdiff

Yet another way to compare files is to use sdiff, which presents the two files onscreen so that you can visually compare them (see Code Listing 6.16).

## To compare files with sdiff:

- sdiff dearliza dearhenry

At the shell prompt, type sdiff and the filenames to compare the two files. The output, as shown in Code Listing 6.16, presents each line of the two files side by side, separating them with

- ▲  if the lines are identical
- ▲ < if the line exists only in the first file
- ▲ > if the line exists only in the second file
- ▲ | if they are different

## ✓ Tips

- If most of the lines are the same, consider using the -s flag so the identical lines are not shown. For example, type sdiff -s dearliza dearhenry.
- If the output scoots by too fast to read, remember that you can pipe the entire command to more, as in sdiff dearliza dearhenry | more.

```
[ejr@hobbes manipulate]$ sdiff dearliza dearhenry
July 25, 1998 July 25, 1998
Dear Liza, Dear Henry,
There's a hole in my bucket, dear Liza, dear Liza, dear Henry.
Liza. I Please fix it dear Henry, dear Henry.
Yours, Yours,
Henry | Liza
| PS, you forgot your toolbox last time.
[ejr@hobbes manipulate]$
```

Code Listing 6.16 sdiff puts the files side by side, so you can easily see the differences.

## Sorting Files with sort

If you want to be really lazy—er, um, smart—let Unix sort files for you. You can use sort to, for example, sort your address book alphabetically—as opposed to the random order in which you might have entered addresses (see Code Listing 6.17).

## To sort files with sort:

- sort address.book > sorted.address.book

To begin, type sort, followed by the name of the file you want to sort. Unix will sort the lines in the file alphabetically and present the sorted results in the file you specify (here, sorted.address.book), as shown in Code Listing 6.17.

```
[ejr@hobbes manipulate]$ more address.book
Schmidt, Sven, 1 Circle Drive, Denver, CO, 80221, 555-555-8382
Feldman, Fester, RR1, Billings, MT 62832, 285-555-0281
Brown, John, 1453 South Street, Tulsa, OK, 74114, 918-555-1234
Smith, Sally, 452 Center Ave., Salt Lake City, UT, 84000, 801-555-8982
Jones, Kelly, 14 Main Street, Santa Clara, CA, 95051, 408-555-7253
[ejr@hobbes manipulate]$ sort address.book
Brown, John, 1453 South Street, Tulsa, OK, 74114, 918-555-1234
Feldman, Fester, RR1, Billings, MT 62832, 285-555-0281
Jones, Kelly, 14 Main Street, Santa Clara, CA, 95051, 408-555-7253
Schmidt, Sven, 1 Circle Drive, Denver, CO, 80221, 555-555-8382
Smith, Sally, 452 Center Ave., Salt Lake City, UT, 84000, 801-555-8982
[ejr@hobbes manipulate]$ sort address.book > sorted.address.book
[ejr@hobbes manipulate]$ cat sorted.address.book
Brown, John, 1453 South Street, Tulsa, OK, 74114, 918-555-1234
Feldman, Fester, RR1, Billings, MT 62832, 285-555-0281
Jones, Kelly, 14 Main Street, Santa Clara, CA, 95051, 408-555-7253
Schmidt, Sven, 1 Circle Drive, Denver, CO, 80221, 555-555-8382
Smith, Sally, 452 Center Ave., Salt Lake City, UT, 84000, 801-555-8982
[ejr@hobbes manipulate]$
```

Code Listing 6.17 An unsorted address book springs to order with the help of sort.

## ✓ Tips

- If you have multiple files to sort, you can use `sort file1 file2 file3 > complete.sorted.file` and the output will contain the contents of all three files—sorted, of course.

- You can sort fields in comma-delimited files by adding `-t` to the command. For example, `sort -t , +1 address.book` tells Unix to sort by the second field. The `-t` and following character (, ) indicate what character separates the fields—the comma in this case. If a character isn’t given, `sort` thinks that white space marks the boundaries between fields. The `+1` says to skip the first field and sort on the second one.

- You can sort numerically, too, with `sort -n filename`. If you don’t use the `-n` flag, the output will be ordered based on the leftmost digits in the numbers—for example "1, 203, 50"—because the alphabetic sort starts at the left of the field.
