# Work with Python

Replace your shell with Python

# What you'll need...

# # Replace your shell with Python

Python is a great programming language, but did you know it can even replace your primary shell?

We all use shell on a daily basis. For most of us, shell is the gateway into our Linux system. For years and even today, Bash has been the default shell for Linux. But it is getting a bit long in the tooth.

No need to be offended we still believe Bash is the best shell when compared to some other UNIX shells such as Korn Shell (KSH), C Shell (CSH) or even TCSH.

This tutorial is not about Bash being incapable, but it is about how to breathe completely new life into the shell to do old things conveniently and new things which were previously not possible, by a long shot. So, without further delay, let's jump in.

While the Python programming language may require you to write longer commands to accomplish a task (due to the way Python's modules are organised), this is not something to be concerned about. You can easily write aliases to the equivalent of Bash command that you intend to replace. Most of the time there will be more than one way to do a thing, but you will need to decide which way works best for you.

Python provides support for executing system commands directly (via the os or subprocess module), but where possible we focus on Python-native implementations here, as this allows us to develop portable code.

# ## SECTION 1: Completing basic shell tasks in Python

# ### 1. File management

The Python module shutil provides support for file and directory operations. It provides support for file attributes, directory copying, archiving etc. Let's look at some of its important functions.

```
shutil module
```