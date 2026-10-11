# Master Vim in easy steps
Learn some advanced features of Vim
TUTORIAL

> For those programmers who want everything automated, Vim also provides an auto-indenting feature

```
mylinuxbook@mylinuxbook-Inspiron-1525:/home/himanshu$ g++ filename1.c
#include <stdio.h>
#include <unistd.h>
// A comment
int main(void)
{
printf("\n Hello World\n");
sleep(10);
return 0;
}

```

+   **9.** This is a better technique than indenting each line, but you still need to count the number of lines to indent. This could prove frustrating, especially if the number of lines is very large.

Fortunately, there is another trick: to select the lines by working with Vim in visual mode. In order to do this, you first need to bring Vim into visual mode. This (as mentioned previously) can be done using **V**. Once in visual mode, use the arrow keys to select all the lines that you want to indent in one go. After this, all you need to do is press **B** or **L** and the whole selected area will be indented accordingly.

+   **10.** Automatic indentation
+   For those programmers who want everything automated, Vim also provides an auto-indenting feature. For example, to enable auto-indenting for C code, use **set autoindent** and **set cindent**. Now, try writing some C code and you will see that Vim automatically produces indentation as you write it.
+   Sometimes, depending upon the existing settings of your Vim editor, lines might get indented to a number of spaces other than four spaces or any other default value that you desire. As a solution to this, you can set the number of spaces to indent using

**set shiftwidth=<number-of-spaces>** For example, simply type **set shiftwidth=4** to indent lines by four spaces.

+   **11** Search words
+   To search for a word in the active window, simply type **/** (search keyword). This will enable Vim's search mode and find the first occurrence of the searched keyword.
+   Use **N** (just press **N** in order to search more occurrences of the keyword). Note that you cannot do a backward search here.
+   If you need to do a backward search then just type **?** (search keyword). This will enable Vim's backward search mode. Again, use **N** to continue the search, but backwards this time.
+   Sometimes the keyword is present in the text/source file and it is desired to find other occurrences of that word in the current text/source file. In this case, just put the cursor below that word and press **T** (or Shift+8). This way, you can search for a word without even typing it.

+   **12** Replace words
+   Vim also supports search and replace operations. To execute a basic replace operation, just type **:s/keyword-to-search/keyword-to-replace/** to replace keyword-to-search with keyword-to-replace-with.
+   This trick is good if you want to replace all the occurrences of a searched keyword, but what if it is desired to replace only selected occurrences? Well, there is a way through which you can run a search and replace operation in interactive mode. This means that Vim will confirm before replacing the keyword each time. This can be done through **: %s/keyword-to-search/keyword-to-replace/g**.

The first occurrence is always highlighted and Vim displays a prompt (in green, at the bottom) where you can input your choice of whether you want to replace this occurrence or not. Here, **y** = Yes, replace this occurrence; **n** = No, skip this occurrence; **a** = Replace this and all other occurrences; **q** = Quit the command; **i** = Replace this match and then quit the command.
Use **Ctrl+e** (^E) and **Ctrl+y** (^Y) to scroll the window up and down in this mode. Also, use **i** and **I** (along with **/c** for, example **/a** or **/ci** for case-insensitive and case-sensitive search.

```
himanshu@mylinuxbook-Inspiron-1525:~
#include <iostream>
class A
{
private:
int a;
int b;
public:
void init()
{
a = 10;
b = a*10;
}
}
replace with char (\d*) (\d*) (\d*) (\d*) (\d*) (\d*) 0,5 Top

```