# ✓ Tips

+   - If you have multiple files to sort, you can use `sort file1 file2 file3 > complete.sorted.file` and the output will contain the contents of all three files—sorted, of course.

+   - You can sort fields in comma-delimited files by adding `-t` to the command. For example, `sort -t , +1 address.book` tells Unix to sort by the second field. The `-t` and following character (, ) indicate what character separates the fields—the comma in this case. If a character isn’t given, `sort` thinks that white space marks the boundaries between fields. The `+1` says to skip the first field and sort on the second one.

+   - You can sort numerically, too, with `sort -n filename`. If you don’t use the `-n` flag, the output will be ordered based on the leftmost digits in the numbers—for example "1, 203, 50"—because the alphabetic sort starts at the left of the field.