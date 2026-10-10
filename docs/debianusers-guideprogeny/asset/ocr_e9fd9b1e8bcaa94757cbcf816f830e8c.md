# The Linux Directory Structure

| Directory | What's In It |
| /var/lock | Lock files that prevent another user from opening or saving particular files. |
| /var/log | Log files for different programs. These logs are invaluable for solving problems. |

# Understanding Absolute and Relative File Paths

A file path is a list of the directories above the file, ending with the file name.

Linux uses two types of paths: absolute and relative paths:

+   - An absolute path always starts with the root directory.
+       For example, the absolute path to a file in a sub-directory in a user's home directory might be `/home/khcong/10100/january.txt`.
+       This path can take a long time to type, but is completely clear.
+   - A relative path starts in your present working directory.
+       For example, if you were in the `/home/khcong` directory, the relative path to a file in a sub-directory might be `10100/january.txt`.
+       You can find your present working directory by using the `pwd` ("present working directory") command.

In addition, `/` indicates the present working directory when you are using the command line.

# Searching from the Desktop

You can search for files or text from the desktop using: