# Try It Live!

We’re going to give you an opportunity to work on your own. In the exercises that follow, we will not give you instructions for every step, as we have done in all previous “Try It Live!” sessions. You will call on what you have already learned to complete some of these steps.

But we understand that Linux is complex; there is a lot to learn and remember. If you need some help refer to the “Try It Live!” Answer Key at the back of this guide. You will find whatever step-by-step instructions we have omitted in the exercises.

+   1. Change to your home directory.
+   2. Create a new directory called **newdir**.
+   3. List your home directory and note the permissions for **newdir**.

```
drwxr-xr-x 1 ronsm 1024 Nov 8 16:00 newdir
drwxrwxr-x 1 ronsm 1024 Mar 1 12:23 practice
```

Figure 8-1 Listing of Your Home Directory

If the permissions that you see on your screen for **newdir** are the same as those you see in Figure 8-1, skip Exercise 4, but do read the explanation following step b.

+   4. If the permissions that you see on your screen for **newdir** are *not* the same as those you see in Figure 8-1, you will change them in this exercise.
+       a. Type `chmod u=rwx,go=rx newdir`
+       b. Press <Enter>

Translating the command syntax in step a into English, we have:
For the user (**u**, the file’s owner), remove whatever permissions now exist (=) and substitute read, write, and execute (**rwx**) permissions for the directory **newdir**.

For both the group and others (**go**), remove whatever permissions now exist (=) and substitute read and execute (**rx**) permissions for the directory **newdir**.