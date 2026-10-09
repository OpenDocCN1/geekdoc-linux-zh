Remember that the `?` wildcard means "exactly one character." The syntax `supply?` means "all files beginning with the characters 'supply' and followed by one and only one character." The file `supp.ly` is not listed in Figure 6-16 because `supply` is followed by two characters.

# Side trip part 3:

Before moving on, you should protect your work by backing it up. As we point out in the CBT course, `tar` and `cpio` are standard Linux utilities that are used to back up files. The guidelines for these two utilities vary from one system to another.

Other backup options include some sort of external device, such as a floppy disk, tape, ZIP or CD-RW drive. We have to assume that none of these devices is available to you, so you will create a subdirectory in your account for this purpose.

+   34. Create a directory called **backup**. (Remember that your working directory is *catalog*, one level below *practice*.)
+       a. Type `mkdir ../backup`
+       b. Press <Enter>

This new subdirectory, **backup**, is a subdirectory of *practice*—not *catalog*.

Let's go through the syntax in step a.

Your working directory is *catalog*. The double dot, `..`, refers to the parent directory, *practice*. The slash is needed to tell the system that you are creating something to be stored in the parent directory. You could have created this new directory by first changing to the directory *practice* and then creating the directory. But that's an extra step.

+   35. Copy the files you created to this safe haven, **backup**.
+       a. Type `cp * ../backup`
+       b. Press <Enter>

The syntax in this example says this: "Copy (`cp`) everything (`*`) to the directory `../backup`, which is a subdirectory of my (*catalog*) parent directory (*practice*)." (Remember that the parent directory is represented by the shorthand double-dot notation.)

Our side trip is now over.