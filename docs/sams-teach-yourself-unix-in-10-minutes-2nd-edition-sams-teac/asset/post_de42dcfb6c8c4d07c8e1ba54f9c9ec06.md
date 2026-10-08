
## Concatenated, What's That? 

Most words in the computer industry can be overwhelming to learn because of what you hear is acronym-based, defined in a complicated way, and so on. In this case, the word concatenate is nothing more than the theory of combining elements for efficiency sake.

In Unix, we use concatenates because Unix has the capability to string or place two or more files to create a single file. Data elements (strings) and contents (files) can be combined together into one element or file. Think of concatenation as the ability to combine things together for ease of use.

The cat command is a byproduct of this definition. The cat command will allow you to concatenate all data specified together into one package.

Now that you are comfortable with the definition and what cat does, let's look at the operation of the cat command. Now, there are a couple of ways to use the cat command. We will look at it in the light of reading files and will touch on it in Lesson 12, “Input and Output,” later in the book. Until then, let's focus on using cat to read files on your system.

To display a file, just supply cat with the file(s) you want to see. If you want to see how powerful Unix is, cat a file like the b1.jpg (JPEG file). Unix will look inside and report back to you. Unix will report in a language you can't read or understand, but this shows that Unix is literal in everything you ask it to do. Unix will do it or crash and die trying!

One example that I am sure you will be able to find on your system is your hosts file located in your /etc directory. I have left out most of the output as the hosts file can be large, but this is exactly one of the main benefits it didn't need to do anything but specify the cat command and either the directory (if I am not in it) and the file.

```
>cat hosts
# This file describes a number of hostname-to-address mappings for the TCP/IP subsystem. It is
# mostly used at boot time, when no name servers are running.
# On small systems, this file can be used instead of a Named server.
# Syntax:
# IP-Address Full-Qualified-Hostname Short-Hostname
#
127.0.0.1 localhost
```

(Output removed)

In this example, while in /etc directory, we used the cat command to view the files for its current entries. We had only one entry because I removed the long stream of output. This can be seen with other commands that we will learn about shortly in this lesson. With cat, you can easily and quickly see the contents of a file.

Another item of importance is that you must know what you can and can't use cat. The cat command will return an error message to you if you try to cat a directory. The error message will tell you that you are trying to cat a directory and that is not allowed. Be aware that cat is for files, not for directories. You can also specify filenames. However, when you receive the results back from your query, you will be given a longer list of the combined concatenates. Do not specify any directories when specifying multiple filenames with the cat command or your query may fail. Also make sure that you test your wildcards and attempt to build them into your cat command queries. For instance, if you want to search for all the files in your /etc directory that may be hosts files, run a query on it, narrow down your search criteria, and cat the file you want to see. You can also cat multiple files.

You can cat all the files simultaneously, but the query results would be large that your results would scroll off the screen too quickly for you to even digest the first sentence shown. Having said that, let's still look at a way to view the entire result so you don't miss anything. First find what you want to look at:

```
>find host*
hosts
hosts.conf
hosts.allow
hosts.deny
```

Since my query looking for host*, everything that starts with the word will be shown with whatever comes after it because of the use of the wildcard. You can then cat your files to see which one is relevant for use.

```
>cat host*
```
This will show you more output than you can possibly even read. We will now move on to managing what you view in a better way, so you can actually read the data! You can use pagers to slow down the output to make it readable.

## Making Output Readable with Pagers

The cat command is fine when you just want to quickly show some information, but what about large files that scroll past a bit too quickly to read and you now can't read them? There is a way to slow down the output of a command like cat, so you can read the data at your speed. Viewing pages one at a time is done with the concept of pagers. Files that scroll the screen will be useless if you need to read the beginning of the file. If the file's size is larger than what can fit on the terminal screen or in your history buffer, you are out of luck. Files are often large enough to do this, and you will still want to read those files. You can use more and less Unix commands. People often refer to more and less by their generic term: pagers. Let's take a quick look at how to use these command-line tools.

## The more Command

All you need to do to use more is to type the command followed by the file or files you want to display. This command is similar to cat. The tricky part is memorizing which one to use and having that knowledge at your fingertips when you need it. Let's take a look at the more command in action:

```
>more hosts.allow
```
(Output removed)

In this example, while in /etc directory, we used the cat command to view the files for its current entries. We had only one entry because I removed the long stream of output. This can be seen with other commands that we will learn about shortly in this lesson. With cat, you can easily and quickly see the contents of a file.

Another item of importance is that you must know what you can and can't use cat. The cat command will return an error message to you if you try to cat a directory. The error message will tell you that you are trying to cat a directory and that is not allowed. Be aware that cat is for files, not for directories. You can also specify filenames. However, when you receive the results back from your query, you will be given a longer list of the combined concatenates. Do not specify any directories when specifying multiple filenames with the cat command or your query may fail. Also make sure that you test your wildcards and attempt to build them into your cat command queries. For instance, if you want to search for all the files in your /etc directory that may be hosts files, run a query on it, narrow down your search criteria, and cat the file you want to see. You can also cat multiple files.

You can cat all the files simultaneously, but the query results would be large that your results would scroll off the screen too quickly for you to even digest the first sentence shown. Having said that, let's still look at a way to view the entire result so you don't miss anything. First find what you want to look at:

```
>find host*
hosts
hosts.conf
hosts.allow
hosts.deny
```

Since my query looking for host*, everything that starts with the word will be shown with whatever comes after it because of the use of the wildcard. You can then cat your files to see which one is relevant for use.

```
>cat host*
```
This will show you more output than you can possibly even read. We will now move on to managing what you view in a better way, so you can actually read the data! You can use pagers to slow down the output to make it readable.

## Making Output Readable with Pagers

The cat command is fine when you just want to quickly show some information, but what about large files that scroll past a bit too quickly to read and you now can't read them? There is a way to slow down the output of a command like cat, so you can read the data at your speed. Viewing pages one at a time is done with the concept of pagers. Files that scroll the screen will be useless if you need to read the beginning of the file. If the file's size is larger than what can fit on the terminal screen or in your history buffer, you are out of luck. Files are often large enough to do this, and you will still want to read those files. You can use more and less Unix commands. People often refer to more and less by their generic term: pagers. Let's take a quick look at how to use these command-line tools.

## The more Command

All you need to do to use more is to type the command followed by the file or files you want to display. This command is similar to cat. The tricky part is memorizing which one to use and having that knowledge at your fingertips when you need it. Let's take a look at the more command in action:

```
>more hosts.allow
```
(Output removed)

In this example, while in /etc directory, we used the cat command to view the files for its current entries. We had only one entry because I removed the long stream of output. This can be seen with other commands that we will learn about shortly in this lesson. With cat, you can easily and quickly see the contents of a file.

Another item of importance is that you must know what you can and can't use cat. The cat command will return an error message to you if you try to cat a directory. The error message will tell you that you are trying to cat a directory and that is not allowed. Be aware that cat is for files, not for directories. You can also specify filenames. However, when you receive the results back from your query, you will be given a longer list of the combined concatenates. Do not specify any directories when specifying multiple filenames with the cat command or your query may fail. Also make sure that you test your wildcards and attempt to build them into your cat command queries. For instance, if you want to search for all the files in your /etc directory that may be hosts files, run a query on it, narrow down your search criteria, and cat the file you want to see. You can also cat multiple files.

You can cat all the files simultaneously, but the query results would be large that your results would scroll off the screen too quickly for you to even digest the first sentence shown. Having said that, let's still look at a way to view the entire result so you don't miss anything. First find what you want to look at:

```
>find host*
hosts
hosts.conf
hosts.allow
hosts.deny
```

Since my query looking for host*, everything that starts with the word will be shown with whatever comes after it because of the use of the wildcard. You can then cat your files to see which one is relevant for use.

```
>cat host*
```
This will show you more output than you can possibly even read. We will now move on to managing what you view in a better way, so you can actually read the data! You can use pagers to slow down the output to make it readable.

## Making Output Readable with Pagers

The cat command is fine when you just want to quickly show some information, but what about large files that scroll past a bit too quickly to read and you now can't read them? There is a way to slow down the output of a command like cat, so you can read the data at your speed. Viewing pages one at a time is done with the concept of pagers. Files that scroll the screen will be useless if you need to read the beginning of the file. If the file's size is larger than what can fit on the terminal screen or in your history buffer, you are out of luck. Files are often large enough to do this, and you will still want to read those files. You can use more and less Unix commands. People often refer to more and less by their generic term: pagers. Let's take a quick look at how to use these command-line tools.

## The more Command

All you need to do to use more is to type the command followed by the file or files you want to display. This command is similar to cat. The tricky part is memorizing which one to use and having that knowledge at your fingertips when you need it. Let's take a look at the more command in action:

```
>more hosts.allow
```
(Output removed)

In this example, while in /etc directory, we used the cat command to view the files for its current entries. We had only one entry because I removed the long stream of output. This can be seen with other commands that we will learn about shortly in this lesson. With cat, you can easily and quickly see the contents of a file.

Another item of importance is that you must know what you can and can't use cat. The cat command will return an error message to you if you try to cat a directory. The error message will tell you that you are trying to cat a directory and that is not allowed. Be aware that cat is for files, not for directories. You can also specify filenames. However, when you receive the results back from your query, you will be given a longer list of the combined concatenates. Do not specify any directories when specifying multiple filenames with the cat command or your query may fail. Also make sure that you test your wildcards and attempt to build them into your cat command queries. For instance, if you want to search for all the files in your /etc directory that may be hosts files, run a query on it, narrow down your search criteria, and cat the file you want to see. You can also cat multiple files.

You can cat all the files simultaneously, but the query results would be large that your results would scroll off the screen too quickly for you to even digest the first sentence shown. Having said that, let's still look at a way to view the entire result so you don't miss anything. First find what you want to look at:

```
>find host*
hosts
hosts.conf
hosts.allow
hosts.deny
```

Since my query looking for host*, everything that starts with the word will be shown with whatever comes after it because of the use of the wildcard. You can then cat your files to see which one is relevant for use.

```
>cat host*
```
This will show you more output than you can possibly even read. We will now move on to managing what you view in a better way, so you can actually read the data! You can use pagers to slow down the output to make it readable.

## Lesson 7

## The less Command

Using the less command is similar to using the cat and more commands. As a matter of fact, the syntax is nearly identical. It's really what the tool does makes it different. When using the less command, you have more control over the pager than ever before.

Here is a good example of the differences between more and less:

```
>more hosts.allow
```
If you try to use the arrow keys for navigation while using the more command, you will find that you can only move forward through the file with the Spacebar. There is not a back and forth as there is with the less command. Now try the same things using the less command:

```
>less hosts.allow
```
You can move up and down the file using your arrow keys. You can even move to the right buffer if you are working on a terminal emulation program like telnet or secure shell. Either way, if you are connected to a Unix system and use more or less, check them out and see what they can do for you. Other options that come with less are similar to those that come with cat and more. The Spacebar always moves you through the file via the page, and q will give you the ability to quit out of the program.
