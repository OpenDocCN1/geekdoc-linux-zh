
# C language Apache modules
# MySQL server with C client library interfaces
# GD graphics library with C interfaces
# Incidental use of CSS, (X)HTML, XML, JavaScript, Ajax

This course has been designed for and lab-tested by first and second year Computer Science Students at Kingston University, London UK.

# SETTING UP YOUR SYSTEM

This book presumes you are using the Linux operating system with either a KDE or Gnome desktop. Specific set-up instructions for common architectures are at http://www.ubiq.org/CProgrammingInLinux/

If you are using the KDE desktop you will have Konqueror or Dolphin as the File Manager and kate or kedit for an editor

In Gnome you would probably use Nautilus and gedit

You need to be familiar with the idea of doing some things as “super user” so that you have access permission to copy or edit certain files. This is normally done by prefacing the Linux command with “sudo” and providing the password, as in this example:

“sudo cp hello3 /srv/www/cgi-bin/hello3”

which copies the file “hello3” to the area where the Apache server locates common gateway interface or cgi programs.

In KDE “kdesu konqueror” would open a file manager as super user.

In Gnome “gnomesu nautilus” would open a file manager as super user.

You will need to have installed the following packages:

| Package | Ubuntu | Open Suse |
| :--- | :--- | :--- |
| C development libraries | build-essential | Base Development (pattern) |
| Apache web server | apache2 | Web and LAMP Server (pattern) |
| Apache development libraries | apache2-prefork-dev | apache2-devel |
| MySQL server, client and development libraries | mysql-server libmysqlclient-dev | libmysqlclient-devel |
| GD and development libraries | libgd2-xpm libgd2-xpm-dev | gd gd-devel |

Throughout the text you will see references to the folder **cgi-bin**. The location of this will vary between Linux distributions. By default this folder used for web programs is:

- OpenSuse: `/srv/www/cgi-bin`
- Ubuntu: `/usr/lib/cgi-bin`

To place programs there you need superuser rights, so it may be better to create a folder inside your own home/`*****`/public\_html/cgi-bin directory and change the **ScriptAlias** and associated **Directory** references inside the Apache configuration files (OpenSuse) `/etc/apache2/default-server.conf` or (Ubuntu) `/etc/apache2/sites-available/default.`

# 1 HELLO WORLD

## 1.1 HELLO PROGRAM 1

Using the File Manager (in KDE, Konqueror or in Gnome, Nautilus) create a new directory somewhere in your home directory called something appropriate for all the examples in this book, perhaps “Programming_In_Linux” without any spaces in the name.

Open an editor (in KDE, kate, or in Gnome, gedit) and type in (or copy from the supplied source code zip bundle) the following:

```c
/*
C Programming in Linux (c) David Haskins 2008
chapter1_1.c
*/
#include <stdio.h>

int main(int argc, char *argv[])
{
    printf("Hello, you are learning C!\n");
    return 0;
}
```

Save the text as **chapter1_1.c** in the new folder you created in your home directory.

Open a terminal window and type: **gcc -o hello chapter1_1.c** to compile the program into a form that can be executed.

Now type “ls -l” to list the details of all the files in this directory. You should see that chapter1_1.c is there and a file called “hello” which is the compiled C program you have just written.

Now type: **./hello** to execute, or run the program and it should return the text:

“Hello you are learning C!”.

If this worked, congratulations, you are now a programmer!

### Anatomy of the program

The part inside /*** *** /is a comment and is not compiled but just for information and reference.

The “#include...” part tells the compiler which system libraries are needed and which header files are being referenced by this program. In our case “printf” is used and this is defined in the stdio.h header.

The “int main(int argc, char *argv[])” part is the start of the actual program. This is an entry-point and most C programs have a main function.

The “int argc” is an argument to the function “main” which is an integer count of the number of character string arguments passed in “char *argv[]” (a list of pointers to character strings) that might be passed at the command line when we run it.

A pointer to some thing is a name given to a memory address for this kind of data type. We can have a pointer to an integer: int *iptr, or a floating point number: float *fPtr. Any list of things is described by [], and if we know exactly how big this list is we might declare it as [200]. In this case we know that the second argument is a list of pointers to character strings.

Everything else in the curly brackets is the main function and in this case the entire program expressed as lines.

Each line or statement end with a semi-colon “;”.

We have function calls like “printf(…)” which is a call to the standard input / output library defined in the header file stdio.h.

At the end of the program “return 0” ends the program by returning a zero to the system.

Return values are often used to indicate the success or status should the program not run correctly.

## 1.2 HELLO PROGRAM 2

Taking this example a stage further, examine the start of the program at the declaration of the entry point function: int main(int argc, char *argv[])

In plain English this means:

The function called “main”, which returns an integer, takes two arguments, an integer called “argc” which is a count of the number of command arguments then *argv[] which is a list or array of pointers to strings which are the actual arguments typed in when you run the program from the command line.

**Some Definitions:**

- **function**: a block of program code with a **return data type**, a name, some arguments of varying data types separated by commas, enclosed in **brackets**, then the body of the function enclosed in **curly brackets**, each statement ending with a **semi-colon**.
- **integer symbol int**: a counting number like 0,1,2,3,4,5.
- **list, array symbol []**: a sequence of things of the same kind in a numbered order.
- **pointer symbol \***: a memory address locating the start of piece of data of a certain type.
- **string or char \***: a pointer to a sequence of characters like 'c', 'a', 't' making up “cat”. A character string ends with a special character NULL or '\0' ascii value 0 or hex 00

Let’s rewrite the program to see what all this means before we start to panic.

```c
/*************************************************
 C Programming in Linux (c) David Haskins 2008
 chapter1_2.c
 *************************************************/
#include <stdio.h>

int main(int argc, char *argv[])
{
 int i=0;
 printf("Hello, you are learning C!\n");
 printf("Number of arguments to the main function:%d\n", argc);
 for(i=0; i<argc; i++)
 {
 printf("argument number %d is %s\n", i, argv[i]);
 }
 return 0;
}
```

Save the text as **chapter1_2.c** in the same folder.

Open a terminal window and type:

```bash
gcc -o hello2 chapter1_2.c
```

to compile the program into a form that can be executed.

Now type `ls -l` to list the details of all the files in this directory. You should see that chapter1_2.c is there and a file called `hello2` which is the compiled C program you have just written.

Now type `./hello2` to execute, or run the program and it should return the text:

```text
Hello, you are still learning C!!
Number of arguments to the main function:1
argument number 0 is ./hello2
```

We can see that the name of the program itself is counted as a command line argument and that the counting of things in the list or array of arguments starts at zero not at one.

Now type `./hello2 my name is David` to execute the program and it should return the text:

```text
Hello, you are still learning C!!
Number of arguments to the main function:5
argument number 0 is ./hello2
argument number 1 is my
argument number 2 is name
argument number 3 is is
argument number 4 is David
```

So, what is happening here? It seems we are reading back each of the character strings (words) that were typed in to run the program.
