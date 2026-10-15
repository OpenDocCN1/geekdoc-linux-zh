```
perror("Fork failed");
exit(1);
}
nbytes = strlen(Child_Greeting);
if (pid == 0) {
    close(data_channel[0]);
    nw = write(data_channel[1], Child_Greeting, nbytes);
    if (nw == -1) {
        perror("Write error");
        exit(1);
    }
    exit(0);
}
/* Parent process */
close(data_channel[1]);
nr = read(data_channel[0], buf, nbytes);
if (nr == -1) {
    perror("Read error");
    exit(1);
}
nw = write(1, buf, nr);
if (nw == -1) {
    perror("Write to stdout failed");
    exit(1);
}
printf("Well done, son!\n");
exit(0);
}
```

```
% gcc46 pipe_talk.c -w -o pipetalk
% ./pipetalk
Hello, mom!
Well done, son!
%
```

# 20.4.2.3 Two-Way Communication

We now discuss a program in which the reader and writer processes carry out two-way communication using two pipes. The pipe_2way_talk.c program opens two pipes, pipe1 and pipe2, and creates a child process. The child process sends a message to the parent process using pipe1 and reads the parent's response from pipe2. The parent does it the other way round. Whatever data the parent and child processes read from their respective pipes, they throw to standard output. Figure 20.5 shows the setup in a pictorial form.

```
% cat pipe_2way_talk.c
#include <unistd.h>
#define SIZE 32
```