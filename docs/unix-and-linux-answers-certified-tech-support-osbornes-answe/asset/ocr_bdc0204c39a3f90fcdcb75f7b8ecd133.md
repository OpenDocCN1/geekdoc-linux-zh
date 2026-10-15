how to get input from a file (rather than the keyboard) can be helpful too. Piping, the most important kind of redirection in UNIX, allows you to take the output of one program and redirect it to another program, which can save you an enormous amount of time and effort.

Even before there was MS Windows, UNIX was a fully functional multitasking operating system. The key to multitasking in UNIX is knowing how to manage all those programs or jobs you're running simultaneously.

It's extremely important to understand how to set priorities when you're working in a UNIX environment, since you're almost always sharing memory capacity and processor time with others. Here's how to be nice.

Scheduling jobs is another way to be courteous to your fellow users and to improve your own efficiency. You can put a job to sleep until later, schedule a job for a specific time in the future, or use a crontab to automate your tasks.

# RUNNING A SINGLE PROGRAM

# Executing a File

Actually, UNIX is always running several programs, so you can't ever just run a single program. But most of that happens in the background and behind the scenes, so we'll just let it stay there for the moment. You'll remember from Chapter 3 that each file on your machine has a set of permissions. These include the permission to read the file, write to the file, and to execute it. By "execute" we mean to make the file run, as in actually do something.

It's important to understand that very few programs, and probably none you will have to worry about unless you end up as a superuser, are actually executed directly by UNIX. This is done by the shell. Whether you are running Bourne, Korn, C, or one of the less common shells, it's actually the shell that interprets what you type at the prompt and issues the necessary commands to start up the program. It's also the responsibility of the shell to examine the permissions for the file and decide if you even have the right to run the program. So, if you don't first set the execute permission bit for your program, you aren't going to get very far with it.