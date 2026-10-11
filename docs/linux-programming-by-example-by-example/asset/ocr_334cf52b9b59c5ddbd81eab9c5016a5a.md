make program, which automates the software-building process. The final chapter of this part of the book discusses the program you will build at the end of the book, a music CD database manager. The programming project will use many of the techniques and tools covered in the book.

> **THE CODE FOR THIS BOOK**
> 
> To see the code for this book, go to [www.mcp.com/info](http://www.mcp.com/info) and type **0 7 8 9 7 2 2 1 5 1** (this book’s ISBN) to get to the Linux Programming by Example Web site.

Part II, “System Programming,” devotes five chapters to low-level Linux programming. Processes are the first subject because they are the key to understanding how any Linux program works. You will learn what a process is, how to create, manipulate, and kill them, and how processes interact with file ownership and access to system resources. The next chapter (Chapter 5) explains what signals are, how to create your own custom signal handlers, and how to ignore signals.

System programming often involves interacting with and requesting services from the kernel. System calls provide the interface between your application code and the kernel, so this is covered in Chapter 6. Chapters 7 and 8 are devoted to Linux file handling. Everything (almost) in Linux is a file, so all but the simplest programs will need file services. The first of these chapters (Chapter 7) provides basic information on file permissions, including creating, opening, closing, and deleting files, and getting information about files.

Chapter 8 goes into advanced file-handling topics, such as interacting with the Linux filesystem, ext2, high-speed I/O using memory maps, and file locking. Finishing up this part is a chapter on writing *daemons*, which are programs that run non-interactively in the background and provide services on request or perform other tasks. Daemons have special requirements, and Chapter 9 shows you what they are and how to meet them.

The third part of the book, “Linux APIs,” takes you through some of the key application programming interfaces (APIs) available on Linux. The database API is the first topic because most applications need to store data in some sort of ordered, easily retrievable fashion. The Berkeley DB database meets that need.

Chapters 11 and 12 focus on manipulating character mode screens using the ncurses API. Chapter 11 looks at basic ncurses usage: initialization, termination, output, and input. Chapter 12 looks at the advanced capabilities ncurses provides, such as using color, window management, interacting with mice, and creating and using forms and menus.

Chapter 13 covers the sound API integrated into the Linux kernel. Finally, Chapter 14, “Creating and Using Programming Libraries,” closes this part of the book. All the APIs discussed are implemented via libraries, so knowing how