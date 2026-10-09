has 262 programs in it. I installed every one of them, either directly or indirectly. Most are small, simple programs that do only one task. This array of small tools makes Unix extremely flexible and adaptable. Many commercial software packages try to do everything; they wind up with all sorts of capabilities but only mediocre performance in their core functions. Remember, at one time you needed to be a programmer to use a Unix system, let alone run one. Programmers don’t mind building their own tools. The Unix concept of pipes encouraged this.

# ### Pipes

People used to GUI environments, such as Windows and macOS, are probably unfamiliar with how Unix handles output and input. They’re used to clicking something and seeing either an OK message, an error, nothing, or (all too often) a pretty blue screen with nifty high-tech letters explaining in the language called *Geek* why the system crashed. Unix does things a little differently.

Unix programs have three channels of communication, or *pipes*: standard input, standard output, and standard error. Once you understand how each of these pipes works, you’re a good way along to understanding the whole system.

*Standard input* is the source of information. When you’re at the console typing a command, the standard input is the data coming from the keyboard. If a program is listening to the network, the standard input is the network. Many programs can rearrange standard input to accept data from the network, a file, another program, the keyboard, or any other source.

The *standard output* is where the program’s output is displayed. This is frequently the console (screen). Network programs usually return their output to the network. Programs might send their output to a file, to another program, over the network, or anywhere else available to the computer.

Finally, *standard error* is where the program sends its error messages. Frequently, console programs return their errors to the console; others