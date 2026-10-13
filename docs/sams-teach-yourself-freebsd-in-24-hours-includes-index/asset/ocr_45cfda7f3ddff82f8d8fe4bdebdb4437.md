+   - How to install software from source code
+   - How to remove installed software from the system
+   - How to manage existing applications
+   - How to work with Linux applications in FreeBSD

# FreeBSD’s Software Packaging Systems

FreeBSD has two different systems that can be used to install software. One of the systems works with prepackaged software that has already been built in to executable binary format. The other system downloads and builds the source code on-the-fly while installing the software. Both systems have their advantages and disadvantages.

# The Differences Between Packages and Ports

As mentioned previously, packages are prebuilt binaries that you can install on your system. This is the type of software most users will be familiar with because it is similar to the way software is delivered for Windows or Macintosh. The main advantage of installing software from packages is that it can often be much quicker than installing from the alternative for two primary reasons. The first is that you avoid the time required to compile and build the software from source code. Although building the software from source does not require a lot of your time, it is a time-consuming process for the computer.

The other advantage of prebuilt packages is that it often requires far less download time. The reason is that building from source requires you to have all the libraries for the C and C++ compiler that the application requires. Any missing libraries have to be downloaded and installed before the application can be installed. In addition, some of these libraries will depend on other libraries, and so on. Although this process is usually automated in its entirety (FreeBSD automatically checks for missing dependencies and installs any that are missing), it can still eat up a lot of download time—especially if you do not have broadband access to the Internet.

However, installing from packages also has its disadvantages. The first one is that not all software is available in packages, so sometimes the only option is to build the software from the source code.

The other disadvantage is that you cannot customize the software or optimize it for your particular processor type. With packages, you are pretty much stuck with whatever options the package maker decided should exist in the software.