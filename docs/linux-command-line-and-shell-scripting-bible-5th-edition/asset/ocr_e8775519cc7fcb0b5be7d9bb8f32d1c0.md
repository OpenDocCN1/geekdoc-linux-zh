# # CHAPTER 15
# Presenting Data

# ## IN THIS CHAPTER

+   *   Understanding input and output
+   *   Redirecting output in scripts
+   *   Redirecting input in scripts
+   *   Creating your own redirection
+   *   Listing open file descriptors
+   *   Suppressing command output
+   *   Using temporary files
+   *   Logging messages

So far the scripts shown in this book display information either by echoing data to the monitor or by redirecting data to a file. Chapter 11, “Basic Script Building,” demonstrated how to redirect the output of a command to a file. This chapter expands on that topic by showing you how you can redirect the output of your script to different locations on your Linux system.

# ### Understanding Input and Output

So far, you’ve seen two methods for displaying the output from your scripts:

+   *   Displaying output on the monitor screen
+   *   Redirecting output to a file

Both methods produced an all-or-nothing approach to data output. There are times, however, when it would be nice to display some data on the monitor and other data in a file. For these instances, it comes in handy to know how Linux handles input and output so that you can get your script output to the right place.

The following sections describe how to use the standard Linux input and output system to your advantage, to help direct script output to specific locations.