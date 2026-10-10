
can do that there is a long list of command-line options available, which can become somewhat imposing.

For most bundling operations, three basic option groups are commonly used for the tar command:

- `-cvf`: Create a new tar file
- `-tvf`: Display the contents of a tar file
- `-xvf`: Extract the contents of a tar file

To create a new tar archive file, specify the output file name and then the list of files and folders to bundle, as shown in the example in Listing 13.1.

## Listing 13.1: Using the tar command to bundle files

```bash
$ tar -cvf test.tar test1.txt test2.txt test3.txt
test1.txt
test2.txt
test3.txt
$ ls -al
total 32
drwxr-xr-x  2 rich rich  4096 Dec  5 08:33 .
drwxr-xr-x 19 rich rich  4096 Dec  5 08:28 ..
-rw-r--r--  1 rich rich   795 Dec  5 08:19 test1.txt
-rw-r--r--  1 rich rich  1020 Dec  5 08:19 test2.txt
-rw-r--r--  1 rich rich  2280 Dec  5 08:20 test3.txt
-rw-r--r--  1 rich rich 10240 Dec  5 08:33 test.tar
$
```

In Listing 13.1, test.tar is the name of the archive file you want to create. For the input files and folders, you can use wildcard characters to specify the names, or even redirect a listing of files to the tar command, making it very versatile in scripts. One of the advantages of bundling folders with tar is that it preserves the folder structure of your environment, including file and folder ownership, making it easier to extract the files and re-create the original environment.

> **TIP**
> Though not required, it's become somewhat of a de facto standard in Linux to use a .tar filename extension to identify a tar archive file. This is commonly called a tarball in Linux circles.

If you need to see what's in a tar archive file, use the -tvf option group:

```bash
$ tar -tvf test.tar
-rw-r--r-- rich/rich    795 2018-12-05 08:19 test1.txt
-rw-r--r-- rich/rich   1020 2018-12-05 08:19 test2.txt
-rw-r--r-- rich/rich   2280 2018-12-05 08:20 test3.txt
$
```

Notice that both the file owner ships and the file permissions are retained within the tar archive file. When you extract the files onto another system, they'll be assigned to the user id that matches the user number assigned to the original files.

Extracting the files and folders from a tar file is just a matter of using the -xvf option group:

```bash
$ tar -xvf test.tar
test1.txt
test2.txt
test3.txt
$ ls -al
total 32
drwxr-xr-x 2 rich rich 4096 Dec 5 08:38 .
drwxr-xr-x 20 rich rich 4096 Dec 5 08:38 ..
-rw-r--r-- 1 rich rich 795 Dec 5 08:19 test1.txt
-rw-r--r-- 1 rich rich 1020 Dec 5 08:19 test2.txt
-rw-r--r-- 1 rich rich 2280 Dec 5 08:20 test3.txt
-rw-r--r-- 1 rich rich 10240 Dec 5 08:38 test.tar
$
```

The tar archive method makes bundling files for distribution easy, but it does tend to create a very large file, which can be awkward to handle. Linux developers usually compress the final tar archive file using some type of file compression utility.

In Linux there is a plethora of ways to create compressed files. Table 13.1 lists the most popular methods you'll run into.

## Table 13.1 Linux compression methods

| **Method** | **Filename extension** | **Description** |
|---|---|---|
| bzip2 | .bz2 | Improvement to the gzip method that reduces file sizes |
| compress | .Z | The original Unix compress utility |
| gzip | .gz | Fast compression method that produces moderate-sized files |
| xz | .xz | Creates smaller compressed files but can be very slow |

By far the most common zip utility used in Linux for tar archive files is the GNU gzip package. To compress a single file, use the gzip command with the filename, as shown in Listing 13.2.

## Listing 13.2: Compressing a tar archive file

```bash
$ gzip test.tar
$ ls -al
total 24
drwxr-xr-x 2 rich rich 4096 Dec 5 08:53 .
drwxr-xr-x 20 rich rich 4096 Dec 5 08:39 ..
-rw-r--r-- 1 rich rich 795 Dec 5 08:19 test1.txt
-rw-r--r-- 1 rich rich 1020 Dec 5 08:19 test2.txt
-rw-r--r-- 1 rich rich 2280 Dec 5 08:20 test3.txt
-rw-r--r-- 1 rich rich 204 Dec 5 08:33 test.tar.gz
$
```

As seen in Listing 13.2, `gzip` adds a `.gz` filename extension to the end of the file that’s compressed.

![](img/c0a399aca0d18f8822d714ad0a173123_463_0.png)

> Often with compressed tar archive files, you’ll see developers shorten the .tar.gz filename extension pair to just .tgz.

To decompress a compressed tarball and extract the original files, you have a couple of options. One option is to use a two-step approach. First use the gunzip command directly on the compressed tar file:

```bash
$ gunzip test.tar.gz
```

This restores the original `test.tar` file. Then you extract the tar file using the standard `-xvf` options of the `tar` command.

The second option is to decompress and extract the tarball file in one step by just adding the `-z` option to the `tar` command line:

```bash
$ tar -zxfv test.tgz
test1.txt
test2.txt
test3.txt
$ ls -al
total 24
drwxr-xr-x 2 rich rich 4096 Dec 5 09:03 .
drwxr-xr-x 3 rich rich 4096 Dec 5 09:02 ..
-rw-r--r-- 1 rich rich 795 Dec 5 08:19 test1.txt
-rw-r--r-- 1 rich rich 1020 Dec 5 08:19 test2.txt
-rw-r--r-- 1 rich rich 2280 Dec 5 08:20 test3.txt
-rw-r--r-- 1 rich rich 204 Dec 5 09:02 test.tgz
$
```

![](img/c0a399aca0d18f8822d714ad0a173123_464_0.png)

One important thing to note is that when you use the gzip program directly, it removes the compressed file and replaces it with the original file, but when you use the `-z` option with the tar command, it retains the compressed file along with decompressing and extracting the original files.

# Compiling Source Code

Once you have the source code package files downloaded onto your Linux system, you’ll need to compile them to create an executable file to run the application. Linux supports a wide variety of programming languages, so you’ll need to know just what programming language the application was written in. Once you know that, you’ll need to install a *compiler* for the program code. A compiler converts the source code into an executable file the Linux system can run.

The most common tool used for compiling programs in Linux is the *GNU Compiler Collection* (gcc). While originally created to support only the C programming language, *gcc* now supports an amazing array of different programming languages, such as Ada, C++, Fortran, Go, Java, Objective-C, Objective-C++, and OpenMP.

![](img/c0a399aca0d18f8822d714ad0a173123_464_1.png)

Most Linux distributions don’t include the *gcc* program by default, so most likely you’ll need to install it on your Linux system. For Ubuntu, it’s part of the *build-essentials* package, while for Rocky Linux you’ll find it in the *Development Tools* package group.

To compile simple one-file programs, just run the *gcc* command-line command against the source code file to produce the executable file that you run on your system. The *-o* option allows you to specify the name of the compiled output file; otherwise it defaults to the ugly *a.out* filename:

```bash
$ cat hello.c
#include <stdio.h>
int main() {
    printf("Hello, this is my first C program!\n");
    return 0;
}
$ gcc -o hello hello.c
$ ./hello
Hello, this is my first C program!
$
```

As mentioned earlier, most larger applications require additional header and library files besides the source code files to build the final application file. Depending on just how many source code, header, and library files are required for an application, the *gcc* command process can get very long and complicated. Separate library files need to be compiled in the proper order before the main program file can be compiled, creating a difficult road map to follow to generate the application.

There’s a simple solution available for you to help keep track of all that. The **make** utility allows developers to create scripts that guide the compiling and installation process of application source code packages so that even novices can compile and install an application from source code.

Usually there are three steps involved with installing an application that uses a **make** script:

1. Run the `configure` utility, which analyzes your Linux system and customizes the **make** script to build the application for your environment.
2. Run the **make** utility by itself to build the necessary library files and executable files for the application.
3. Run **make install** as the root user account to install the application files in the appropriate locations on your system.

What makes C language programs so complicated is that they often split the application functions into separate library files. Each library file contains one or more specialized functions used in the application code.

The benefit of splitting functions into separate library files is that multiple applications that use the same functions can share the same library files. These files, called *shared libraries*, make it easier to distribute applications but more complicated to keep track of what library files are installed with which applications.

While not necessary for compiling the application source code, the `ldd` utility can come in handy if you need to track down missing library files for an application. It displays a list of the library files required for the specified application file:

```bash
$ ldd hello
    linux-vdso.so.1 (0x00007fff7df40000)
    libc.so.6 => /lib64/libc.so.6 (0x00007fe154e57000)
    /lib64/ld-linux-x86-64.so.2 (0x00007fe15521c000)
$
```

My simple **hello** application requires two external library files, the standard **linux-vdso.so.1** and **libc.so.6** files, which provide the ability for the `printf()` function to display the output. The **ldd** utility also shows where those files were found on the Linux system. That in itself can be helpful when troubleshooting issues with applications picking up the wrong library files.

# Packaging Applications

While the **tar**, **gcc**, and **make** programs make it easier to distribute, compile, and install application source code, that’s still somewhat of a messy process for installing new applications. For most Linux users, all they want to do is download an application and use it.
