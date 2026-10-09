
Let’s look at a hypothetical example that illustrates these points better. Say you decide to develop an application that needs to monitor hard disk partitions and alert an administrator if the amount of available space drops below ten percent. The application must also determine who is occupying the most space and send them an e-mail urging them to clean up by listing their fifteen largest files. What would happen if we were to try to develop this using a shell scripting language, like bash? First, we would start out using the df command, which returns a report of the disk space usage. The report could be something like the following, depending on how your machine is partitioned:

```
Filesystem          1K-blocks       Used  Available Use% Mounted on
/dev/hda1             3020140     1582492    1284232  56% /
/dev/hda5             7684844     1280812    6013656  18% /data
/dev/hda2             3020172     2637411    229341   92% /home
none                   94868           0      94868   0% /dev/shm
```

We would then need to extract the percentage values from this report, which is more difficult than it seems; most shell scripting languages don’t support this type of text manipulation directly. As a result, we would need to use a language such as sed or awk to get at the data that we are looking for. sed and awk are languages designed specifically for pattern matching and transformation and are used extensively in shell scripting. Once we determine that the /dev/hda2 partition (the /home filesystem) exceeds the 90 percentage usage threshold, we would need to calculate each user’s individual usage and determine their largest files. How would we do that?

We would need to get a list of all the users’ home directories in the filesystem, most likely using the ls command, and then iterate through each one using a loop of some sort. As we go through each directory, we would issue the du command to get a list of all the files and their sizes, like so:

```
3656 /home/postgres/base/1
3656 /home/postgres/base/16975
4 /home/postgres/base/16976/pgsq1_tmp
1128708 /home/postgres/base/16976
1136024 /home/postgres/base
140 /home/postgres/global
82024 /home/postgres/pg_xlog
12 /home/postgres/pg_clog
1218232 /home/postgres
```

The most difficult part of this process is to keep track of each user’s usage and their files, both the name and the size. Why is this difficult, you may ask? Shell scripting languages have very primitive support for complex logic operations and data structures. We would need to come up with an alternative mechanism to temporarily store this individual data, and then process and sort it once we finish going through all the users’ directories. The final part of the application would involve sending an e-mail, both to the offending users and the administrator, using the mail or sendmail commands.

You may have noticed that we glossed over the section regarding sed and awk earlier. There’s a reason for this – shell scripting languages allow us to develop scripts that invoke shell commands easily and without much effort. In addition, the development cycle is rather simple; we use an editor to modify and debug the script and then simply execute it from the command line. On the other hand, shell scripts fall apart when we need to implement any type of complex logical operations or store relational or structured data, since shell scripting languages were not designed for this purpose.

On the flip side, how would we fare if we developed this application using Perl? We would retain some of the advantages of shell scripting, but also have access to more advanced language features. Since Perl allows us to interact with the shell, we can use the df command to get the disk usage report, and then use pattern matching expressions to easily parse and extract the percentage values. If we find a partition that exceeds the threshold value, we can use the internal readdir function, along with a for loop, to iterate through all of the main directories on that filesystem. Perl integrates well with the underlying operating system to abstract certain functions on all supported platforms. This allows us to use a function like readdir to get a list of all the files in a particular directory, whether we are using Linux or Mac OS X.

For each directory, we can use the df command, like we did before, to get a list of all the individual files and their sizes and then store them in a complex data structure. Once we finish iterating through all the directories, we can use Perl’s sort function to sort and order the information in the data structure to determine the offending users and their largest files. At that point, we can send e-mail to the administrator and the necessary users, either using the external mail or sendmail commands, or a Perl extension such as Mail::Send. Typically, we would want to use an extension, instead of an external shell command, since it is more efficient and allows us to better implement the desired functionality. We’ll actually take a look at how to write this application in Perl later in the chapter, after looking through some simpler examples first.

We won’t go through the advantages or disadvantages of developing a similar application in a compiled language, like C or C++, since it is beyond the scope of this chapter. But, if you are interested in a high-level overview, a language such as C provides more control (i.e. memory management) and typically better performance, but at the expense of development time and difficulty.

Now, let’s take a more in-depth look at the advantages and disadvantages of Perl. This will allow you to evaluate what Perl has to offer for yourself.

## Advantages

As we discussed earlier, Perl provides a good mixture of features and performance that lies somewhere between a scripting language and a compiled language. To understand this better, here are some specific advantages of Perl:

- Perl provides us with great flexibility in developing applications. Perl does not force us to use any specific style or paradigm, but instead allows us to express our ideas and thoughts in the way that we choose. In fact, one of Perl’s mottos is, "*there is more than one way to do it.*"
- Perl is extensible. We can write modules or libraries in Perl to extend its functionality and make them available for reuse in other projects. The Comprehensive Perl Archive Network (CPAN) holds hundreds and thousands of freely available extensions to interface and communicate with various utilities, applications, Internet services and database engines.
- Perl is highly portable and runs on a large number of hardware and software platforms, including most known Unix / Linux platforms, Windows, Mac OS, OS/2, VMS, and even Palm. Programs that don't use platform specific functionality, such as pipes in Unix, or OLE/COM in Windows, will work unchanged across platforms.
- Perl supports powerful regular expressions for pattern matching. We can use these expressions to search for patterns or specific strings in a body of text.
- Perl has a strong developer community, which is very active in implementing extensions, fixing bugs, and providing technical support.
- Perl is free for both commercial and non-commercial use!

## Disadvantages

Like any other programming language, Perl does have its share of disadvantages:

- The flexibility that Perl provides can sometimes mesmerize developers into producing hard to maintain code. Because there are so many different ways to solve the same problem, it's easy to come up with a solution that no one else can follow – especially if your documentation isn't up to scratch.
- Perl has weak exception handling abilities that make it difficult for you to handle any errors that crop up during the execution of your script – for example if a file isn't where it's supposed to be, or if write-access to one of our disks isn't permitted.

However, for the most part, Perl is perfectly capable of doing the tasks that we require of it in a sensible and organized way. We'll begin to look at some examples of this shortly, but before we can do that, we need to make sure that we've got Perl installed correctly.

# Installation

Perl, along with a number of useful modules, is installed by default on your Linux system. We will use the terms extension and module interchangeably, since they have much the same meaning in Perl. If you want to check what version of Perl is installed, use the `perl` command with the `-v` option:

```
$ perl -v
This is perl, v5.8.0 built for i386-linux-thread-multi
(with 1 registered patch, see perl -V for more detail)
```
