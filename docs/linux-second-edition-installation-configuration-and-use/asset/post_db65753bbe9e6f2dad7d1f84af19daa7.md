
# LINUX-SPECIFIC ONLINE DOCUMENTATION 81

You will find late breaking information on security gaps and other problems of the distributions' homepages. Debian manages information on bug reports and their solution (if there is one) for all packages. SuSE maintains a support database that frequently occurring problems and their solutions are described. Besides a search function, there is also an alphabetical index. If, for example, you have problems with ISDN configuration, this is the best place to look for a solution.

```
http://www.debian.org
http://www.redhat.com
http://www.suse.com
```

## Distribution-dependent documentation

One distinctive feature of different Linux distributions is how online documentation is made available. The following list gives a first overview; further information can be found in Appendices A to C of this book where distribution-specific details are described.

- Several distributions come with an extensive installation manual which is available both in printed form and as an online document in various formats (PostScript, HTML).
- Many distributions make their HTML-formatted documentation more accessible by providing a central starting page. (A special mention is deserved by SuSE where, after installation of the appropriate packages, the HTML versions of all man texts, numerous info texts, all HOWTO texts, all SuSE package support database, and many more, can be accessed from one central starting point).
- Some distributions try to facilitate full text search in the existing online documentation by providing additional tools (such as RedHat's helptool)
- Practically all distributions provide daily updated information on their pages (see above).

## Part II: Configuration

## Linux fundamentals 5

The changeover from DOS or any other Unix-compatible operating system to Linux frequently causes difficulties. Many of these difficulties are due to the fact that, on the surface, Linux has many similarities to other operating systems, although there are substantial differences in its internal structure and administration. This chapter attempts to look behind the scenes, describing the basic Linux features.

The first part of this chapter mainly contains information about several levels of the Linux tile file system: from handling files and directories (including the use of wildcards, access privileges, links) to the structure of the Linux directory tree (FSTND) and the so-called I-nodes which Linux uses internally for data administration.

Subsequent sections deal in more depth with Linux internals, and their contents will probably make full sense only once you have become better acquainted with Linux. They deal with the specifics of process management (Linux being a multitasking system), the administration of libraries and the System V Init process (which controls startup and shutdown of your computer).

This chapter is not strictly necessary for the configuration of Linux — since the following chapters describe the procedures step by step. But this chapter will help you understand what you are doing. Such basic understanding of Linux and the way it will become necessary at some point when you want to change the configuration of your computer in such a specific way that a description would no longer fit into the framework of this or other books.

> If you have never worked with a Unix system before, you should at least read Sections 5.1 and 5.4 (page 116). This will probably save you a lot of frustration when Linux does not react in the way you would have expected from your DOS or Windows experience.

## 5.1 Fundamentals of file management

This section sheds some light on different aspects of file management under Linux. The range of subjects goes from fairly trivial issues (file names are allowed) to the internals of file management (I-nodes and so on). This section is intended to help you use the Linux file system as you understand it. The main subjects are:

- Files and directories (file names, wildcards * and ?, directories).
- Linux directory structure (which files are, the meaning of abbreviations such as bin, sbin, lib, usr, home, and so on).
- Ownership and access privileges (who is allowed to read, modify, execute files, administration of users and groups).
- Links and symbolic references to other files and directories.
- Access to several data supports (what the mount command is used for, how CD-ROMs and floppy disks are linked into the Linux file system).
- Import and export of DOS text files (end-of-line characters (CR+LF under DOS, LF only under Linux), foreign language characters).
- Different file systems (which different file systems exist, such as ext2 (Linux standard), msdos, iso9660 (CD-ROM), and so on).
- Internals (how the Linux file system is managed internally, what I-nodes are).

## Files and directories

If you have been working under DOS/Windows, the new freedom for file names will be one of the first things you will like about Linux. Briefly, here are the main facts:

- Under Linux, file names can be up to 255 characters long.
- Linux is case sensitive.
- Special characters are allowed; however, specific rules must be followed when handling such files.
- Files whose names start with a dot (full stop) are considered hidden files (page 90).

This last point needs some additional comments: you may use any number of dots in file names. In Linux file names, the dot is a character like any other, even though it is frequently used to separate parts of names. README.bootils.gz is a completely normal file name which suggests that it is a compressed README file on the subject of boot utilities.

File names which are not immediately recognizable as such when entering commands (such as file names containing spaces) must be enclosed in double quotes (for example, "a b"). It is even possible to use foreign language special characters, such as German umlauts or accented letters. You should, however, be aware that these special characters are a potential source of trouble, the least that can happen is file names containing special characters are not sorted properly by ls.

> Linux supports various file systems, among others the MS-DOS file system. The above remarks are only valid for the Linux standard file system ext2. Other file systems have stronger restrictions regarding the maximum number of characters in file names and so on (see also page 105).

## Wildcards

In your standard use of files, you will frequently work on whole groups of files – for example, all files ending in .tex. In order to make this possible, two wildcards are allowed when entering Linux commands: ? to specify any arbitrary character, and * to specify any number (including zero) of characters.

On the surface, this looks exactly the same as under DOS. In reality, however, wildcards under Linux are significantly more flexible than under DOS. The most important difference is that * matches nearly all files, including dots (dots) as they are not the first character of a file name). If you want to include all files, you just specify * and not .* as under DOS. (Notes on hidden files later.)

A further difference is that several wildcards do not throw Linux off balance names – With *graph*, for example, you can search for all files that contain graph in their names an underscore, e.g. graphics.doc appgraph, and README.graph.

If the wildcards ? and * are too general for your purpose, you can achieve stronger restrictions by using square brackets. [abc] is a placeholder for one of the three letters a, b. or c. If within square brackets, a hyphen is specified between two letters or digits, then this stands for a character between them: [a-f]* comprises all files begins containing a letter between a and f. [.-]* stands for all files that somewhere in their names contain at least an underscore, or a hyphen. [!a-z]* means all files that begin with an uppercase letter or a special character. *.[Ch3] comprises all files ending in .c or .h.

Wildcards can also be used for directories. /*. includes all *.tex located in the current directory (only one level, then no files in sub-directories), /usr/*/bin/* includes all files in the directories /usr/bin and /usr/sbin.

When files are copied, another special character is frequently needed – the dot as a placeholder for the current directory. The command cp project/*..c copies all *.c files in the project directory into the current directory.

## Wildcards for file names

| Symbol | Description |
| :--- | :--- |
| ? | exactly one arbitrary character |
| * | exactly one number (including zero) of arbitrary characters |
| [abc] | exactly one of the specified characters |
| [a-f] | one character out of the specified range |

![](img/b30873dd3d753687a59253fb9ad26a0b_114_0.png)
