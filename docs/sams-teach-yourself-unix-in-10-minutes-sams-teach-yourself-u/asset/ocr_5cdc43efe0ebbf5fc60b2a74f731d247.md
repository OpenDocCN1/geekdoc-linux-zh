Your computer produces a file named joe.uue, which when decoded by Joe is named hijoe and contains the contents of your sendtojoe file.

Now you can copy and paste, or include, or do whatever you need to do to insert the file you just created into an email message and send it wherever you want.

Of course, if you receive a uuencoded file, you need to know how to decode the file. Decoding a uuencoded file is also extremely simple; issue the uudecode command as `uudecode <filename.uue>`.

Your machine will produce a file in the current directory identical to the one originally uuencoded.

> **Clearing up .uue** The filename of the .uue file and the filename to which it will decode itself do not have to be the same. This is sometimes confusing. If you receive a file named kludge.uue, issue the uudecode kludge.uue command, and do not find a file named kludge in your directory, don't be alarmed. The uuencoded file contains the filename as well as the uuencoded file contents. To find out what the uudecoded file will be named, use the head command to look at the first few lines of the uuencoded file. The filename to which it will decode appears on the first line.

# KDE ARCHIVING TOOLS

Desktop environments also now provide convenient drag-and-drop file compression and archiving tools. The KDE environment, for example, provides the KZip archive and compression tool.

To access the KZip tool, click the K on the KDE toolbar, choose Utilities from the pop-up menu and Zip from its submenu. A window similar to the one shown in Figure 10.1 will appear.