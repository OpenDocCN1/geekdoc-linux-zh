you can move from section to section of the documentation for a program. Type `info info` to learn more about this system.

Both man pages and info pages are usually written in a terse style. They're intended as reference tools, not tutorials; they frequently assume basic familiarity with the command, or at least with Linux generally. For more tutorial information, you must look elsewhere, such as this book or the Web. The Linux Documentation Project (http://tldp.org) is a particularly relevant Web-based resource for learning about various Linux topics.

# # Using Streams, Redirection, and Pipes

Streams, redirection, and pipes are some of the more powerful command-line tools in Linux. Linux treats the input to and output from programs as a stream, which is a data entity that can be manipulated. Ordinarily, input comes from the keyboard and output goes to the screen (which in this context can mean a full-screen text-mode login session, an xterm or a similar window, or the screen of a remote computer via a remote login session). You can redirect these input and output streams to come from or go to other sources, though, such as files. Similarly, you can pipe the output of one program into another program. These facilities can be great tools to tie together multiple programs.

> Part of the Unix philosophy to which Linux adheres is, whenever possible, to do complex things by combining multiple simple tools. Redirection and pipes help in this task by enabling simple programs to be combined together in chains, each link feeding off the output of the preceding link.

# ## Exploring Types of Streams

To begin understanding redirection and pipes, you must first understand the different types of input and output streams. Three are most important for this topic:

+   * **Standard input** Programs accept keyboard input via *standard input*, or stdin. In most cases, this is the data that comes into the computer from a keyboard.

+   * **Standard output** Text-mode programs send most data to their users via *standard output* (a.k.a. stdout), which is normally displayed on the screen, either in a full-screen text-mode session or in a GUI window such as an xterm. (Fully GUI programs such as GUI word processors don't use standard output for their regular interactions, although they might use standard output to display messages in the xterm from which they were launched. GUI output isn't handled via an output stream in the sense I'm describing here.)

+   * **Standard error** Linux provides a second type of output stream, known as *standard error*, or stderr. This output stream is intended to carry high-priority information such as error messages. Ordinarily, standard error is sent to the same output device as standard output,