
### 13.5 Suggested Reading

- 1. *C, A Reference Manual, 5th edition*, by Samuel P. Harbison III and Guy L. Steele, Jr., Prentice-Hall, Upper Saddle River, New Jersey, USA, 2002. ISBN: 0-13-089592-X.
  We have mentioned this book before. It provides a concise and comprehensible description of the evolution and use of the multibyte and wide-character facilities in the C standard library. This is particularly valuable on modern systems supporting C99 because the library was significantly enhanced for the 1999 C standard.
- 2. *GNU gettext tools*, by Ulrich Drepper, Jim Meyering, François Pinard, and Bruno Haible. This is the manual for GNU *gettext*. On a GNU/Linux system, you can see the local copy with `info gettext`. Or download and print the latest version (from `ftp://ftp.gnu.org/gnu/gettext/`).

### 13.6 Summary

- Program internationalization and localization fall under the general heading of *native language support*. *i18n*, *l10n*, and *NLS* are popular acronyms. The central concept is the *locale*, which customizes the character set, date, time, and monetary and numeric information for the current language and country.
- Locale awareness must be enabled with `setlocale()`. Different locale categories provide access to the different kinds of locale information. Locale-unaware programs act as if they were in the `"C"` locale, which produces results typical of Unix systems before NLS: 7-bit ASCII, English names for months and days, and so on. The `"POSIX"` locale is equivalent to the `"C"` one.
- Locale-aware string comparisons are done with `strcoll()` or with the combination of `strxfrm()` and `strcmp()`. Library facilities provide access to locale information (`localeconv()` and `nl_langinfo()`) as well as locale-specific information formatting (`strfmon()`, `strftime()`, and `printf()`).
- The flip side of retrieving locale-related information is producing messages in the local language. The System V `catgets()` design, while standardized by POSIX, is difficult to use and not recommended. Instead, GNU gettext implements and extends the original Solaris design.
  - With gettext(), the original English message string acts as a key into a binary translation file from which to retrieve the string’s translation. Each application specifies a unique text domain so that gettext() can find the correct translation file (known as a “message catalog”). The text domain is set with textdomain(). For testing, or as otherwise needed, the location for message catalogs can be changed with bindtextdomain().
  - Along with gettext(), variants provide access to translations in different text domains or different locale categories. Additionally, the ngettext() function and its variants enable correct plural translations without overburdening the developer. The positional specifier within printf() format specifiers enables translation of format strings where arguments need to be printed in a different order from the one in which they’re provided.
  - In practice, GNU programs use the gettext.h header file and _() and N_() macros for marking translatable strings in their source files. This practice keeps program source code readable and maintainable while still providing the benefits of i18n and l10n.
  - GNU gettext provides numerous tools for the creation and management of translation databases (portable object files) and their binary equivalents (message object files).
  - Finally, it pays to be aware of character set and encoding issues. Software vendors can no longer afford to assume that their users are willing to work in only one language.

### Exercises

1. Does your system support locales? If so, what is the default locale?
2. Look at the *locale*(1) manpage if you have it. How many locales are there if you count them with '`locale -a | wc -l`'?
   ¹³ GNU/Linux supports it, but only for compatibility.
3. Experiment with `ch13-strings.c`, `ch13-lconv.c`, `ch13-strfmon.c`, `ch13-quoteflag.c`, and `ch13-times.c` in different locales. What is the most "unusual" locale you can find, and why?
4. Take one of your programs. Internationalize it to use GNU `gettext`. Try to find someone who speaks another language to translate the messages for you. Compile the translation, and test it by using `bindtextdomain()`. What was your translator's reaction upon seeing the translations in use?

# Chapter 14

![](img/766b5597246d532412fad21b1c59ccec_561_0.png)

In this chapter

- 14.1 Allocating Aligned Memory: posix_memalign() and memalign()
  - page 530
- 14.2 Locking Files
  - page 531
- 14.3 More Precise Times
  - page 543
- 14.4 Advanced Searching with Binary Trees
  - page 551
- 14.5 Summary
  - page 562
- Exercises
  - page 563

This chapter describes several extended APIs. The APIs here are similar in nature to those described earlier in the book or provide additional facilities. Some of them could not be discussed easily until after the prerequisite topics were covered. The presentation order here parallels the order of the chapters in the first half of the book. The topics are not otherwise related to each other. We cover the following topics: dynamically allocating aligned memory; file locking; a number of calls that work with subsecond time values; and a more advanced suite of functions for storing and retrieving arbitrary data values. Unless stated otherwise, all the APIs in this chapter are included in the POSIX standard.

## 14.1 Allocating Aligned Memory: posix_memalign() and memalign()

For most tasks, the standard allocation routines, malloc(), realloc(), and so on, are fine. Occasionally, though, you may need memory that is aligned a certain way. In other words, the address of the first allocated byte is a multiple of some number. (For example, on some systems, memory copies are significantly faster into and out of word-aligned buffers.) Two functions offer this service:

```c
#include <stdlib.h>

int posix_memalign(void **memptr, size_t alignment, size_t size); POSIX ADV
void *memalign(size_t boundary, size_t size); Common
```

posix_memalign() is a newer function; it’s part of yet another optional extension, the “Advisory Information” (ADV) extension. The function works differently from most other allocation Linux APIs. It does not return -1 when there’s a problem. Rather, the return value is 0 on success or an errno value on failure. The arguments are as follows:

- **void \*\*memptr**
  A pointer to a void * variable. The pointed-to variable will have the address of the allocated storage placed into it. The allocated storage can be released with free().
- **size_t alignment**
  The required alignment. It must be a multiple of sizeof(void *) and a power of 2.
- **size_t size**
  The number of bytes to allocate.

memalign() is a nonstandard but widely available function that works similarly. The return value is NULL on failure or the requested storage on success, with *boundary* (a power of 2) indicating the alignment and *size* indicating the requested amount of memory.

Traditionally, storage allocated with memalign() could *not* be released with free(), since memalign() would allocate storage with malloc() and return a pointer to a suitably-aligned byte somewhere within that storage. The GLIBC version does not have this problem. Of the two, you should use posix_memalign() if you have it.

## 14.2 Locking Files

Modern Unix systems, including GNU/Linux, allow you to lock part or all of a file for reading and writing. Like many parts of the Unix API that developed after V7, there are multiple, conflicting ways to do file locking. This section covers the possibilities.

### 14.2.1 File Locking Concepts

Just as the lock in your front door prevents unwanted entry into your home, a *lock* on a file prevents access to data within the file. File locking was added to Unix after the development of V7 (from which all modern Unix systems are descended) and thus, for a while, multiple, conflicting file-locking mechanisms were available and in use on different Unix systems. Both BSD Unix and System V had their own incompatible locking calls. Eventually, POSIX formalized the System V way of doing file locks. Fortunately, the names of the calls were different between System V and BSD, so GNU/Linux, in an effort to please everyone, supports both kinds of locks.

Table 14.1 summarizes the different kinds of locks.

There are multiple aspects to locking, as follows:

#### Record locking

A record lock is a lock on a portion of the file. Since Unix files are just byte streams, it would be more correct to use the term *range lock* since the lock is on a range of bytes. Nevertheless, the term “record lock” is in common use.
