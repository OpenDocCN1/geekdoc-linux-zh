After the option **SO_OOBINLINE** has been enabled, the out-of-band data will be received with the normal data. In this manner, the out-of-band data received is indistinguishable from the normal data.

# Options SO_PASSCRED and SO_PEERCRED

These options are applicable to **PF_UNIX** (**PF_LOCAL**) sockets only. These are used to control and pass credentials on sockets that are local to the current host machine. The discussion of credentials will be deferred until Chapter 17, "Passing Credentials and File Descriptors." This is perhaps the most difficult topic for you to master in this book. For now, simply note that these two options are likely to be of interest to you if you plan to write server programs that serve clients on the same local host.

# What's Next

In this chapter, you learned that socket options can be fetched and set using the functions **getsockopt(2)** and **setsockopt(2)**, respectively. It was shown that socket options have levels and various **SOL_SOCKET** level options were discussed.

Many options required Boolean values, which are defined in the **int** data type. It was shown that some other options such as **SO_LINGER**, for example, required a special structure to be used instead.

A number of socket options relate to advanced uses of sockets, which have not been covered yet. You will see these options again, as the more advanced topics are encountered in the chapters that follow. The next chapter discusses broadcasting with UDP, and consequently you are now prepared to enable the **SO_BROADCAST** option and use it!