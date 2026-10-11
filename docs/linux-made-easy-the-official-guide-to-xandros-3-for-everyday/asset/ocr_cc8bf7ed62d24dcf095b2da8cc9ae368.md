Risk comes as ZIP archive, so once the download is complete, you will have to unzip the file using the double-click-then-copy-and-paste method you learned in Chapter 5. Once finished, you will have a new folder, Risk, within your Home folder. If you take a look in that folder, you will notice the file Risk.jar. This is the game itself that you will be running via the command line. In the future, should you choose to download other Java-based applications, the file with the .jar extension will be the one you will be trying to run.

# 20C-2: Running Risk

You can now run Risk without any further work. To get going, open a new Console window and do the following:

+   1. Move your Console into the Risk folder by typing cd Risk and pressing ENTER.

+   2. Then type java -jar Risk.jar (be sure to place a space between java and -jar) and press ENTER. Risk will appear, and you can start playing.

![](bbox=[0.2, 0.45, 0.78, 0.8])

*Figure 20-9: Risk*

Here’s what you just did in that last line: the first part of the command string, *java*, calls the Java Runtime Environment into action; the *-jar* flag after that tells Java that you are going to be running a .jar file; and the last part is the actual file you are going to run, *Risk.jar*. In the future, if you choose to run other Java-based applications, just follow the same pattern: *java -jar application_name.jar*.