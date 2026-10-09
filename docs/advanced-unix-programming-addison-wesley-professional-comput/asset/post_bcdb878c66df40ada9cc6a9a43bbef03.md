
- All the copying of data from files to sockets (in and out of the process's memory) is very time consuming. It would be a killer for 10,000 clients.
- Lots of other internal tables and other resources that our server might use start running out of space, or slowing way down, or both.

So, as you can see, the problems get pretty serious. This is one reason why a real Web server (or any other large-capacity server) is a hugely complex piece of software.

If you’re trying to handle 10,000 clients, or even 500, there’s a terrific article titled “The C10K Problem” that explains the problem and surveys most of the possible solutions [Keg2003].

## Exercises

- **8.1.** Modify the multiple-client example in Section 8.1.3 to work between computers (AF_INET). Run the server on one computer and run clients on at least one other computer.

- **8.2.** Based on the information in [RFC1288], implement a simple version of the `finger` command, without options other than the user@host argument. Use connected sockets (`SOCK_STREAM`). For the next Exercise, you might need an option to set the port number.

- **8.3.** Also based on [RFC1288], implement a simple `finger` server, but use an unused high-numbered port (e.g., 3079) instead of the standard port 79. Use connected sockets. Test your server with the `finger` command you wrote in the previous Exercise. If you have a machine you can play with, install your server on port 79 and test it with a standard `finger` command running on another machine.

- **8.4.** Same as Exercise 8.2, but with connectionless sockets.

- **8.5.** Same as Exercise 8.3, but with connectionless sockets.

- **8.6.** Design and try to implement a simple communication example based on RFC 2549, which you can find at [RFC]. You may restrict yourself to the Concorde and First quality-of-service levels.

- **8.7.** Implement a graphical Web browser using a GUI toolkit such as Qt. Warning: This is really hard! You may want to do this as a semester-long group project. Hint: Start your design with a way to handle nested tables. If you get that part right, everything else is relatively easy.

- **8.8.** Implement the SMI with connectionless sockets, instead of with connected sockets as we did in Section 8.5. Run some timing tests like those in Section 7.15.

- **8.9.** Implement a web crawler that starts with some URL and then scans what it finds there to discover additional URLs (e.g., by looking for strings that start with "href"). It adds the discovered URLs to a list, and then scans them, discovering even more URLs. It stops when it's found some specified number of URLs or when it's interrupted. (Obviously, it needs to continue when it encounters an error.) There should be a way to display the results—at least all the URLs discovered and whether they were scanned successfully (HTTP status of 200) or not and, if not, what the reason was. You *must* implement the Robot Exclusion Protocol (see www.robotstxt.org for details) so you don't crawl onto pages that you've been requested to stay away from. Provide a "unique host" option that crawls each host (the part of the URL up to the first slash) only once, using whatever URL was tried first for that host (e.g., www.basepath.com/index.htm). Using that option, try to find a starting URL that yields the most unique hosts that are successfully scanned. (I thought starting with www.yahoo.com would be a good idea, but I got exactly one hit because all the links there were relative to www.yahoo.com.) Be nice to others when you run your crawler by making sure that you're not hogging network resources.

- **8.10.** Extend the program you wrote in Exercise 5.14 to include process attributes from Appendix A that are explained in this chapter.

## 9 Signals and Timers

### 9.1 Signal Basics

A signal is a notification that an event has occurred, such as a user typing an interrupt (Ctrl-c, normally), a floating-point exception, or an alarm going off. Usually, a signal is delivered to a process or thread asynchronously and whatever the process or thread is doing is interrupted. The signal might immediately terminate the process, or, by prearrangement, a function designated to catch it might be executed.

#### 9.1.1 Introduction to Signals

To show how a program handles a signal, here’s a simple example of a program that displays a number once every three seconds, but when an interrupt signal occurs, it displays a message and terminates:

```c
static void fcn(int signum)
{
    (void)write(STDOUT_FILENO, "Got signal\n", 11);
    _exit(EXIT_FAILURE);
}

int main(void)
{
    int i;
    struct sigaction act;

    memset(&act, 0, sizeof(act));
    act.sa_handler = fcn;
    ec_negl( sigaction(SIGINT, &act, NULL) );

    for ( i = 1; ; i++ ) {
        sleep(3);
        printf("%d\n", i);
    }
    exit(EXIT_SUCCESS);

EC_CLEANUP_BGN:
    exit(EXIT_FAILURE);
EC_CLEANUP_END:
}
```

The call to `sigaction` installed a signal-handling function for the `SIGINT` signal. When I ran this program, I typed a Ctrl-c after a “2” appeared. That caused whatever the program was doing (perhaps sleeping, or inside `printf`, or just looping) to be interrupted and the function `fcn` to be called immediately. It displayed a message and terminated the program with a call to `_exit`. (See Section 9.1.7 for why I didn’t use `exit`.)

The output on the screen was:

```
1
2
Got signal
```

If I hadn’t installed the signal handler, typing Ctrl-c would have terminated the process right away. Technically, the reason is that the default action for the `SIGINT` signal is to terminate the process.

I also could have called `sigaction` to arrange for `SIGINT` signals to be ignored:

```c
int main(void)
{
    int i;
    struct sigaction act;

    memset(&act, 0, sizeof(act));
    act.sa_handler = SIG_IGN;
    ec_negl( sigaction(SIGINT, &act, NULL) );

    for ( i = 1; ; i++ ) {
        sleep(3);
        printf("%d\n", i);
    }
    exit(EXIT_SUCCESS);

EC_CLEANUP_BGN:
    exit(EXIT_FAILURE);
EC_CLEANUP_END:
}
```

This time it kept displaying numbers, and typing Ctrl-c had no effect. We finally terminated it by typing Ctrl-\, which generated a quit signal (`SIGQUIT`), whose default behavior, which we didn’t modify, is to terminate the process.

Well, so much for the basics. Signals are actually pretty complicated because:

- There are lots of different signals, and sometimes the circumstances under which they’re generated and what they mean are complicated.
- Arranging the appropriate action for a signal can be complicated.
- Handling a signal can be complicated.

I’ll go through the issues step-by-step, and when you’ve finished this chapter all will be clear.

### 9.1.2 A Signal’s Lifecycle

A signal is born when whatever event it’s associated with occurs and *generates* it. Its life ends when it is *delivered*, which means that whatever *action* specified for it has been taken. There are three possible actions:

1. Default action (*SIG_DFL*): terminate, stop, or continue the process, or ignore the signal.
2. Ignore the signal (*SIG_IGN*).
3. Catch the signal by executing a signal handler when the signal is delivered.

Most signals can be generated *naturally* by whatever user or system event the signal is associated with. For example, dividing by zero generates a *SIGFPE* event naturally, and termination of a child generates a *SIGCHLD* event naturally. Alternatively, any signal can be generated *synthetically* by one of five system calls: *kill*, *killpg*, *pthread_kill*, *raise*, or *sigqueue*. The next section, which enumerates all the signals, indicates the natural cause of each signal that has one. Five signals, *SIGKILL*, *SIGSTOP*, *SIGTERM*, *SIGUSR1*, and *SIGUSR2* have no natural cause and exist only to be synthesized, usually with the *kill* system call.

Between generation and delivery a signal is *pending*. If another signal of the same type arrives while a signal is pending, whether multiple signals of the same type are delivered is implementation dependent and should not be assumed in portable programs. There’s more on this subject in Section 9.5.3.
