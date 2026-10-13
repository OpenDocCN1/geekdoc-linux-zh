**Shell Variations** If you're using another shell, be aware that redirection is one of the places where syntax varies significantly. Check the man pages for the shell of your preference to learn more.

# PIPES

Not only can UNIX redirect STDIN and STDOUT from and to files, but because these are data streams to UNIX it also provides the idea of piping these streams directly between different programs. With pipes you can use the STDOUT of one program directly as the STDIN of another.

To create a pipe in UNIX, you simply use a | character between the programs on the command line.

Again, using an example is so much more illustrative than a lot of words. Take the example of your compulsive collecting of your Web server log-files. If, instead of collecting them in files, you want to amuse and amaze all your friends by sending them the tail end of the file (using email is discussed in Lesson 18, "Accessing the Network Resources"), you can do so without saving it in a file by using the following command:

```
> tail -30 /usr/local/httpd/logs/access_log | mail
```

Thus far, your repertoire of UNIX commands probably isn't large enough to make this a truly useful feature of you, but as you learn more about UNIX you will find it a powerful tool for simplifying your tasks.

For now, one way in which you can make this feature work for you is by piping things into pagers. For example, if you want to be able to page through the output of the ls command, you can pipe it into more. Try typing the following:

```
> ls -lRaF / | more
```

You see a particularly long listing of files; if you don't eventually press Ctrl+c to get out of this list, it can go on for days. Because this is really a complete recursive listing of your entire filesystem in long format, you're not going to use this particular ls command too often. But any time you want to page through an ls listing—or any other program output that flows off your screen—you can pipe it into more.