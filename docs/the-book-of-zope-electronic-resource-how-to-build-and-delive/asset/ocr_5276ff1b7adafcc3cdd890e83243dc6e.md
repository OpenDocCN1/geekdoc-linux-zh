+   * Modularize your code. Write short code blocks and keep the code in a single object or file manageable in size. It is much easier to debug small, logical parts of a program than one written as a single huge file.

+   * Proofread your code and test it in your mind before running it to make sure you have not skipped any steps or misspelled or misplaced names.

+   * Write "sanity checks" into your code to do this in Python is to convert arguments explicitly to the desired type before acting on them (use the float()), int(), str(), and list() functions for this purpose.

These basic principles of good programming style will serve you well when it comes to debugging.

# 16.2.3 Intermittent Errors

The most difficult to find and fix are intermittent ones. Intermittent errors are often ignored because they happen only rarely and are therefore more difficult to notice or reproduce. But not fixing intermittent errors immediately will only cause you more problems, because as a program ages it becomes more difficult for the programmer to understand the code. So fix all errors as soon as you learn about them.

To find intermittent errors, first try to reproduce it by creating a situation in which it occurred. Once you create the error at all, you will probably have discovered the cause of the error—or at least found a solid clue.

In Zope, both the standard Python error messages and Zope-specific error messages may occur, as discussed in the following sections.

# 16.2.4 Standard Python Error Messages

Table 16-1 lists the standard Python error messages that may also occur when you are working with Zope.

# 16.2.5 DTM Error Messages

To debug DML code, you will often need to use a different procedure to find the error. Each time you create or modify an object, Zope performs a syntax check. If an error is found during this check, the object is neither created nor modified, and you will need to click the Back button to return to edit mode for the object. You must resolve all syntax errors before you can create, modify, or test an object.

With exceptions, Zope error messages all have the same format (see Figure 16-1). They begin with the name of the tag that caused the error ("No closing tag") followed by the name of the tag that caused the error ("for tag <dtml-in>") and the location of the error ("on line 4 of index.html").