```
}

/* server (readfd, writefd); */
size = strlen(message1);
if ((n = read(readfd, buff, size)) == -1) {
    perror ("server read");
    exit (1);
}
if (write (1, buff, n) < n) {
    perror("server write1");
    exit (1);
}
size = strlen(message2);
if (write (writefd, message2, size) != size) {
    perror ("server write2");
    exit (1);
}
close (readfd);
close (writefd);
}
```

Figure 20.7 shows the compilation and execution of the client-server model by using two terminal windows on our system. We compile the client.c and server.c programs and save the executable codes in the client and server files, respectively. We then run the server program in Window 1, followed by running the client program in Window 2. The client process sends the "Hello, world!" message to the server process through FIFO1 and then waits for a message from the server process. The server process receives the client message and displays it on standard output. It then sends the "Hello, class!" message to the client process through FIFO2, closes both FIFOs, and exits. The client process receives the message and displays it on the screen. It then closes both FIFOs and removes them from the file system. Figure 20.8 shows the pictorial representation of the running of the client-server model.

The client-server model discussed is for communication between two processes running on the same machine. In this case, the communication is an exchange of one message each from client to server and vice versa. The model may be extended to the exchange of multiple messages between the two processes. You can extend this model such that the server process may serve multiple clients. Figure 20.9 shows the general view of such a model.

![](bbox=[0.25, 0.9, 0.75, 0.95])

FIGURE 20.7 Compilation and running of the client-server model in two terminal windows.