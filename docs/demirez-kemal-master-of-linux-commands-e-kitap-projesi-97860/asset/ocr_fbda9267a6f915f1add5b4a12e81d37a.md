We said we have several ways to set up programs on Linux systems. One of them is, to install the source codes for the program, compile them and install. Command pattern used for this, as follows:

```
././configure
make
make install
```

The source code is contained within the submitted package readme, install, etc. such places should be examined. Eventhoun general installation pattern should be one as above, sometimes it can be installed from the console by running the install scripts. While we are in files that contain the source code of the software to be installed, for example if the file is in the home folder, with cd <source_code_file>, we can use ./configure, make and make install commands and our program will be installed.

# Tasksel

To set up various server programs and other packages in our system, we can use tasksel tool. When we use the tasksel command from the console, a graphical interface will come as follow.