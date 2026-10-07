# Appendix A

# Changes between 2.0 and 2.2

I don't know the entire kernel well enough to document all of the changes. In the course of converting the examples (or actually, adapting Emmanuel Papirakis' changes) I came across the following differences. I listed all of them together to help module programmers, especially those who learned from previous versions of this book and are most familiar with the techniques I use, convert to the new version.

An additional resource for people who wish to convert to 2.2 is in http://www.atnf.csiro.au/~rgooch/linux/docs/porting-to-2.2.html.

+   1. asmac.h If you need put_user or get_user you have to #include it.
2. get_user In version 2.2, get_user receives the pointer into user memory and the variable in kernel memory to fill with the information. The reason for this is that get_user can read two or four bytes at a time if the variable we read is two or four bytes long.
3. file_operations This structure now has a flush function between the open and close functions.
4. close in file_operations In version 2.2, the close function returns an integer, so it's allowed to fail.
5. write and read in instead of size_t The headers for these functions changed. They now return ssize_t instead of an integer, and their parameter list is different. The inode is no longer a parameter, and on the other hand the offset into the file.