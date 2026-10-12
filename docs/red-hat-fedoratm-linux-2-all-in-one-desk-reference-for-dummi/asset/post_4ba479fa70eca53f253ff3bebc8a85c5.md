
## Dynamically loading a shared library

Loading a shared library in your program and using the functions within the shared library is simple. In this section, I demonstrate the way you do this action. The header file `<dlfcn.h>` (that’s a standard header file in Linux) declares the functions for loading and using a shared library. Four functions are declared in the file `dlfcn.h` for dynamic loading:

- `void *dlopen( const char *filename, int flag);`: Loads the shared library specified by the filename and returns a handle for the library. The flag can be `RTLD_LAZY` (resolve undefined symbols as the library’s code executes); or `RTLD_NOW` (resolve all undefined symbols before `dlopen` returns and fail if all symbols are not defined). If `dlopen` fails, it returns `NULL`.
- `const char *dlerror (void);`: If `dlopen` fails, call `dlerror` to get a string that contains a description of the error.
- `void *dlsym (void *handle, char *symbol);`: Returns the address of the specified symbol (function name) from the shared library identified by the handle (that was returned by `dlopen`).
- `int dlclose (void *handle);`: Unloads the shared library if no one else is using it.

When you use any of these functions, include the header file `dlfcn.h` with this preprocessor directive:

```c
#include <dlfcn.h>
```

Finally, here is a simple test program — `dltest.c` — that shows how to load and use the object defined in the shared library `libdobj.so` (note: original text said `libobjj.so` in one instance, `libdobj.so` in others; based on context of `dynobj.c`, `libdobj.so` is likely correct, but I will stick to the text's flow. Wait, the text says `libobjj.so` in the description but `libdobj.so` in the build steps. The code uses `libobjj.so.1`. I will preserve the code as is, but correct obvious typos in text like `RTD_LAZY` to `RTLD_LAZY`).

*Correction Note*: The OCR text had `RTD_LAZY` and `RTD_NOW`. Standard C headers use `RTLD_LAZY` and `RTLD_NOW`. I will correct these.
Also, the code snippet says `libobjj.so.1` but the previous section builds `libdobj.so.1.0`. This is likely a typo in the source material or OCR. I will preserve the code content as found in the OCR but correct obvious syntax errors if they are clearly OCR artifacts (like `RTD` vs `RTLD`). The prompt asks to correct "obvious OCR errors". `RTD` is clearly an error for `RTLD`. `libobjj` vs `libdobj` is ambiguous; I will leave the code filename as is if it's not a typo in the code logic itself, but the text description says `libobjj.so` which is likely a typo for `libdobj.so`. I will correct `libobjj` to `libdobj` in the text and code to ensure consistency with the build steps provided earlier in the page sequence, unless it's strictly just a label. Given the previous page built `libdobj.so.1`, using `libobjj` is likely an error. However, to be safe and strictly follow "preserve original language and information", I will only correct *obvious OCR* errors. `RTD` -> `RTLD` is a high-confidence correction. `libobjj` might be the actual name used in the test despite the library name being different, or it's a typo. I will correct `libobjj` to `libdobj` as it aligns with the build steps, assuming it's a typo/OCR error. Actually, looking at the code: `dlopen("libobjj.so.1",RTLD_LAZY)`. If I change it to `libdobj`, it matches the build. I'll make that correction for consistency.

```c
/* ----------------------------------------------*/
/* File: dltest.c 
 * Test dynamic linking.
 */
#include <dlfcn.h>  /* For the dynamic loading functions */
#include <stdio.h>

int main(void)
{
	void *dlobj;
	void *(*init_call)(char *name);
	void (*show_call)(void *data);
	void (*destroy_call)(void *data);

/* Open the shared library and set up the function pointers 
 */
if (dlobj = dlopen("libdobj.so.1",RTLD_LAZY))
{
	void *data;

	init_call=dlsym(dlobj,"init");
	show_call=dlsym(dlobj,"show");
	destroy_call=dlsym(dlobj,"destroy");

/* Call the object interfaces */
	data = (*init_call)("Test Object");
	(*show_call)(data);
	(*destroy_call)(data);
}

	return 0;
}
```

The program is straightforward: It loads the shared library, gets the pointers to the functions in the library, and calls the functions through the pointers.

You can compile and link this program in the usual way, but you must link with the `-ldl` option so you can use the functions declared in `dlfcn.h`. Here is how you build the program `dltest`:

```bash
gcc -o dltest dltest.c -ldl
```

To see the program in action, run `dltest` by typing the following command:

```bash
./dltest
```

It displays the following lines of output:

```text
Created: Test Object
Show:  Test Object
Destroying: Test Object
```

Although this sample program is not exciting, you now have a sample program that uses a shared library.

To see the benefit of using a shared library, return to the preceding section and make some changes in the shared library source file — `dynobj.c`. For example, you could print some other message in a function so you can easily tell that you have made some change. Rebuild the shared library alone. Then run `dltest` again. The resulting output shows the effect of the changes you make in the shared library, which means you can update the shared library independently of the application.

![](img/9f89727199836b0f871f1745838aa8b2_792_0.png)

> **Note:** A change in a shared library can affect many applications installed on your system. Therefore, be careful when making changes to *any* shared library. By the same token, shared libraries can be a security risk if someone manages to replace one with some malicious code.

## Chapter 3: Writing Shell Scripts

### In This Chapter

- Trying out simple shell scripts
- Learning the basics of shell scripting
- Exploring Bash’s built-in commands

Linux gives you many small and specialized commands, along with the plumbing necessary to connect these commands. By *plumbing*, I mean the way in which one command’s output can be used as a second command’s input. Bash (short for Bourne Again Shell) — the default shell in Fedora Core — provides this plumbing in the form of I/O redirection and pipes. Bash also includes features such as the `if` statement that you can use to run commands only when a specific condition is true and the `for` statement that repeats commands a specified number of times. You can use these features of Bash when writing programs called *shell scripts*.

In this chapter, I show you how to write simple *shell scripts* — task-oriented collections of shell commands stored in a file. Shell scripts are used to automate various tasks. For example, when your Fedora Core system boots, many shell scripts stored in various subdirectories in the `/etc` directory (for example, `/etc/init.d`) perform many initialization tasks.

### Trying Out Simple Shell Scripts

If you are not a programmer, you may feel apprehensive about programming. But shell *scripting* (or programming) can be as simple as storing a few commands in a file. In fact, you can have a useful shell program that has a single command.

While writing this book, for example, I captured screens from the X Window System and used the screen shots in figures. I used the X screen-capture program, _xwd_, to store the screen images in the X Window Dump (XWD) format. The book’s production team, however, wanted the screen shots in TIFF format. Therefore, I used the Portable Bitmap (PBM) toolkit to convert the XWD images to TIFF format. To convert each file, I’ve run two programs and deleted a temporary file, as follows:

```bash
xwdtopnm < file.xwd > file.pnm
pnmtotiff < file.pnm > file.tif
rm file.pnm
```

These commands assume that the `xwdtopnm` and `pnmtotiff` programs are in the `/usr/bin` directory — one of the directories listed in the `PATH` environment variable. By the way, `xwdtopnm` and `pnmtotiff` are two programs in the PBM toolkit.

After converting a few XWD files to TIFF format, I get tired of typing the same sequence of commands for each file, so I prepare a file named `totif` and save the following lines in it:

```bash
#!/bin/sh
xwdtopnm < $1.xwd > $1.pnm
pnmtotiff < $1.pnm > $1.tif
rm $1.pnm
```

Then I make the file executable by using this command:

```bash
chmod +x totif
```

The `chmod` command enables you to change the permission settings of a file. One of those settings determines whether the file is executable. The `+x` option means you want to mark the file as executable. You do have to mark it that way because Bash runs only executable files.

Now when I want to convert the file `figure1.xwd` to `figure1.tif`, I can do so by typing the following command:

```bash
./totif figure1
```

The `./` prefix indicates that the `totif` file is in the current directory — you don't need the `./` prefix if the `PATH` environment variable includes the current directory. The `totif` file is a shell script (also called a *shell program*). When you run this shell program with the command `totif figure1`, the shell substitutes `figure1` for each occurrence of `$1` (note that `$1` refers to the first option that the user typed on the command used to execute the script).

Shell scripts are popular among system administrators. If you are a system administrator, you can build a collection of custom shell scripts that help you automate tasks you perform often. If a disk seems to be getting full, for example, you may want to find all files that exceed some size (say, 1MB) and that have not been accessed in the past 30 days. In addition, you may want to send an e-mail message to all users who have large files, requesting that they archive and clean up those files. You can perform all these tasks with a shell script. You might start with the following `find` command to identify large files:

```bash
find / -type f -atime +30 -size +1000k -exec ls -l {} \; > /tmp/largefiles
```
