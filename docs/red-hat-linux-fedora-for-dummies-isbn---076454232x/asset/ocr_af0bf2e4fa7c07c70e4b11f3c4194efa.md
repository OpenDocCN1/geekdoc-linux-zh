The Microsoft Windows operating system provides a platform for running Microsoft applications, such as Word. That platform is a little like an electrical plug that provides the power to run various appliances; the appliances are analogous to applications. What the Windows plug provides is a library of commonly used low-level functions that are referred to as an Application Program Interface (API). Those functions perform tasks common to every application, such as opening a file or talking over a network. Using a common library prevents every single application from having to reinvent the wheel. Instead, the applications just plug into the common "outlet" and concentrate on performing their particular function.

The problem is that the Windows platform, or "plug," has square holes and Linux has round ones. You can't plug Word directly into the Linux operating system, for example. That's where Wine comes in and provides the adapter so that you can plug the round peg into the square hole.

![](bbox=[0.12, 0.4, 0.22, 0.47])

Wine stands for Wine Is Not an Emulator. This typical acronym is the type that Linux and Unix programmers love. The Wine acronym means not only that some people just need to get out more, but also that it doesn't simulate (emulate) the entire Windows environment. Rather, it duplicates the interface between the application and the operating system. Using the electrical plug analogy, Wine doesn't emulate the entire electrical grid (as in Windows) but, rather, simply provides the adapter.

# ## Downloading Wine

Unfortunately, because Red Hat doesn't include Wine in its distribution, you have to download it from the Internet. These steps describe how to do so:

+   1. **Log in to your Red Hat Linux computer as any user.**
   You can log in as the superuser (root) if you want, but that's not necessary. By not logging in as the superuser, you don't run the risk of unintentionally damaging your computer (for example, deleting all your files).
2. **Open your Mozilla browser by clicking the blue globe on the GNOME Menu.**
   Using Mozilla is described in Chapter 11.
3. **Enter the address www.winehq.com in the text box at the top of the browser and press Enter.**
   You go to the Wine project's home page.
4. **Under the Download heading on the center-left side of the Web page, click the Binaries link.**
   Your browser displays the Wine Binary Downloads page. This page contains links to various noncommercial and commercial repositories.