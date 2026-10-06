2. If you don't find the icon for the program you're looking for, try installing the Main Menu application from the Software Center. Once it's installed, start Main Menu and find the application you're looking for by navigating through the menus. Right-click the name of your program and choose Properties from the menu that pops up. When the Launcher Properties window appears, take a look at the contents of the Command—for Tomboy it should tomboy --search (Figure 21-5). You can ignore everything after the first space (only the first part matters), so in this case, the program’s command name is tomboy.

![](bbox=[0.271, 0.237, 0.893, 0.621])

Figure 21-5: Finding the command name for Tomboy using Main Menu

3. With the command name, press ALT-F2 to open the Run command of the Dash again.

4. Type ubuntu-bug tomboy (replacing tomboy with the command name for your program) and press ENTER.

The bug-reporting tool will start and collect some information about the program (such as what version you're using). Next, it'll ask whether you want to send this report to the developers—you do, so click Send Report, and a web page will open (log in to Launchpad if you haven't done so already). Type a brief description of your problem, being as specific as possible, and click Next.

356 Chapter 21