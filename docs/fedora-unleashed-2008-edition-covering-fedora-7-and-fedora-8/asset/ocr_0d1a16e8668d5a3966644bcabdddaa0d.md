popular .NET language. In this list, you’ll see things such as avahi-sharp, dbus-sharp, evolution-sharp, gecko-sharp2, gmime-sharp, gnome-sharp, gtk-sharp2, gtksourceview-sharp, and ipod-sharp—we recommend you at least install the gtk-sharp2 libraries (including the development package) as these are used to create graphical user interfaces for Mono.

But for now, let’s get you up and running with Mono on the command line. Mono is split into two distinct parts: the compiler and the interpreter. The compiler turns your source code into an executable, and is called gmcs. The interpreter actually runs your code as a working program, and is just called Mono. You should by now have installed MonoDevelop, so go to the **Applications** menu, choose **Programming**, then **MonoDevelop** to start it up.

> > **TIP**  
> > You don’t have to use MonoDevelop to write your code, but it helps—syntax highlighting, code completion, and drag-and-drop GUI designers are just a few of its features.

When MonoDevelop has loaded, go to the **File** menu and choose **New Project**. From the left of the window that appears, choose **C#**, then **Console Project**. Give it a name and choose a location to save it—all being well, you should see something similar to Figure 29.1. When you’re ready, click **New** to have MonoDevelop generate your project for you.

![](bbox=[0.08, 0.52, 0.91, 0.85])

FIGURE 29.1 MonoDevelop ships with a number of templates to get you started, including one for a quick Console Project.