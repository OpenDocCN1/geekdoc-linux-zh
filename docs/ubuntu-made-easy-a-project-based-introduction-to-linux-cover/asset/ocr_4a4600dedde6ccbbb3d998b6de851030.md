a bit of time, but don't worry. As long as the mysterious text keeps flowing and you don't get an error message at the very end of the whole process, all will be well.

Once configure has done its thing, you will see your prompt again, and you can go on to the translation, or compilation, step. The command reads the makefile created by configure to see how needs to be set up on your machine. It then proceeds to call on the compiler to translate the high-level source code to low-level, machine-readable files that can be installed in the subsequent step.

+   3. To perform this translation, type make and press ENTER.

Again, you will be treated to even more mysterious text flowing through the window and a short wait, usually a tad longer than for the configure process. Once make has done its job and you see your prompt, you are ready to install the program.

Up to this, you have not changed your system in any way. The changes far have taken place in the xmahjong-3.7 folder only—your system is still as pure as you started. Of course, all is going to end right now when you perform the final installation step.

# 8D-4: Installing and Running Xmahjong

Now you've come to the last step in this part of the process, make install. Here you are telling your system to install what you have created, or compiled, in the make step. Note that because installation takes place in permissions-protected parts of your system, you will need to add sudo to the command string to give yourself administrative privileges.

To perform the installation, type sudo install and press ENTER. You will be prompted for your password. After you type it and press ENTER, the installation process will take place. Once your Terminal brings you to your user prompt, Xmahjong will be installed and ready to run from the Terminal. Just type xmahjong and press ENTER.

# 8D-5: Cleaning Up/Uninstall Xmahjong

Once you are done and everything seems to be working as it should, you would normally tidy up in the Xmahjong folder by getting rid of unnecessary files. You can do this by using the Terminal and the cd command to go back into the Xmahjong folder, typing make clean, and pressing ENTER.

If you want to uninstall Xmahjong, open a Terminal window, go back to the Xmahjong folder using the cd command, type sudo uninstall, and finally press ENTER. The routine is essentially the same for any applications installed in this way, though you might imagine, uninstallation isn't as smooth as a process that I've described (and it's definitely not easy as it is the Ubuntu Software Center).

The main reason for the uninstallation process being less cooperative is that the uninstall requires you to keep the project folder, which means you have to keep a bit of clutter you normally wouldn't need to bother with. On top of this, some projects do not provide a