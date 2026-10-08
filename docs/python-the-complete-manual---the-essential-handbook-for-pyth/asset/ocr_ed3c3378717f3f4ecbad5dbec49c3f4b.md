# Hello World

Let's get stuck in, and what better way than with the programmer's best friend, the 'Hello World' application! Start by opening a terminal. Its current working directory will be your home directory. It's probably a good idea to make a directory for the files that we'll be creating in this tutorial, rather than having them loose in your home directory. You can create a directory called Python using the command mkdir Python. You'll then want to change into that directory using the command cd Python.

The next step is to create an empty file using the command 'touch' followed by the filename. Our expert used the command touch hello_world.py. The final and most important part of setting up the file is making it executable. This allows us to run code inside the hello_world.py file. We do this with the command chmod +x hello_world.py. Now that we have our file set up, we can go ahead and open it up in nano, or alternatively any text editor of your choice. Git is a great editor with syntax highlighting support that should be available on any distribution. You'll be able to install it using your package manager if you don't have it.

```
[liam-iam-laptop]$ mkdir Python
[liam-iam-laptop]$ cd Python/
[liam-iam-laptop Python]$ touch hello_world.py
[liam-iam-laptop Python]$ chmod +x hello_world.py
[liam-iam-laptop Python]$ nano hello_world.py
```

Our Hello World program is very simple, it only needs two lines.
The first line begins with a 'shebang' (the symbol #! – also known