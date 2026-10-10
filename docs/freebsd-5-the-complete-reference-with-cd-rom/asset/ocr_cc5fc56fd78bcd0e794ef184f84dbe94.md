![](bbox=[0.14, 0.09, 0.86, 0.45])

Figure 23-5. The Edit Applications List dialog box shows applications that Nautilus believes are reasonable candidates for handling a document type.

You can now test the file association by locating a file of the specified type in a Nautilus file manager and double-clicking it. If everything worked, the application should launch and open the file. If this doesn’t happen, try the following debugging tricks:

+   In an xterm window, use *ps* to look for the running application. For instance, you might type `ps ax | grep AbiWord` to see if AbiWord is running. You can try running such a command frequently for several seconds after double-clicking a file type to see if the application is starting and then failing. Of course, if it starts and fails very quickly, this test won’t be likely to catch it. If the program is launching and then failing, you may want to try the next debugging procedure to help discover the cause.

+   Try launching the program from an xterm by typing its name. You might also try passing it the name of a data file, as in `AbiWord myfile.awb`, to test the program’s ability to load a file when launched in this way. Launching a program from an xterm may create useful error messages in the xterm window.

+   If you see no evidence that the program is launching at all, double-check that it’s installed and double-check the filename you typed in Step 7 of the previous procedure.

Editing existing file associations is fairly straightforward. A somewhat more complex task is creating an entirely new file association. You might do this if you’ve