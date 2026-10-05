# Chapter 7 · Managing Files

simplify some tasks, such as working with all files with names that include the string invoice. Then you should be familiar with these text-mode commands.

To begin this task, we describe some ways that you can create files. With files created, you can copy them from one location to another. You may also maytimes want to move or rename files. Linux enables you to create links, which are ways to refer to the same file by multiple names. If you never want to use a file again, you can delete it. Wildcards provide the means to refer to many files by using a case-sensitive notation. Finally, we cover the case-sensitive nature of Linux’s file management commands.

# Creating Files

Normally, you create files using the programs that manipulate them. For instance, you might use a graphics program to create a new graphics file. This process varies from one program to another, but GUI programs typically use a menu option called Save or Save As to save a file. Text-mode programs provide similar functionality, but the details of how it’s done greatly from one program to another.

One program deserves special mention as a way to create files: touch. You can type your program’s name followed by the name of a file that you want to create, such as touch newfile.txt to create an empty file newfile.txt. Ordinarily, you don’t need to do this to create a file of a particular type, unless you use a specialized program to do the job. Sometimes, though, it’s helpful to create an empty file just to have the file itself—instance, to create a “scratch” files to test some other command.

If you pass the name of a file that already exists, touch updates that file’s access and modification time stamps to the current date and time. This can be handy if you are using a command that works on files based on their access times, and you want the program to treat an old file as if it were new. You may also want to do this if you want to distribute a collection of files and you want all to have identical timestamps.

You can use a number of options with touch to modify its behavior. The most important of these are as follows:

**Don’t Create a File** The -c or --no-create option tells touch not to create a new file if it doesn’t already exist. This is an option if you want to update time stamps but do not want to create an empty file accidentally, should you mistype a filename.

**Set the Time to a Specific Value** You can use -d or --date=string to set the date of a file to that represented by the specified string, which can take any number of forms. For instance, touch -d "July 4 2015" afile.txt clauses

Chapter 10, “Files,” describes how to create files with the text-mode pico, nano, and vi editors.

Certification Objective

A programmer’s tool known as make compiles source code if it’s new, program sometimes uses touch to force make to recompile a source-file.

![](bbox=[0.038, 0.323, 0.198, 0.353])