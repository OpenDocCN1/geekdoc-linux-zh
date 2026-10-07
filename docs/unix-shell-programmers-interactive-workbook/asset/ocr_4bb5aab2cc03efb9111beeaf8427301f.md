# CHAPTER 3

# TEST YOUR THINKING

The projects in this section are meant to have you utilize all of the skills that you have acquired throughout this chapter.The answers to these projects can be found at the companion web site to this book, located at:

http://www.phpptr.com/phpinteractive/

Visit the web site periodically to share and discuss your answers.

+   1) Write a function named overwrite that copies file_a over file_b, even if file_b exists.

a) Make the function work, no matter how the shell's options are set and without changing the settings of any shell options.

b) Now rewrite the function so that it change the setting of a shell option to do the same thing.

c) How can you see if your answer to Question Ib affects the noclobber setting after you run your functionn
d) You might have written your function starting either overwrite( or overwrite() (.Whichever way you wrote it, now rewrite it using the other form, and answer Question Ic again. (The results should be different.)

e) Discuss the advantages and disadvantages of using >, instead of set +o noclobber inside the two types of functions.

+   2) Write a command Line that reads a file named Months that contains the names of the months, one per line, and writes a new file named mons that contains the three-letter abbreviation for each month.The abbreviations in mons must be all lowercase, regardless of how the names are capitalized in Months.