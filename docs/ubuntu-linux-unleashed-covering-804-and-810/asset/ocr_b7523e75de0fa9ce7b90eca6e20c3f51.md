```
// the Uri of hits is its location, which might
// be on the web, on your filesystem, or somewhere else
Console.WriteLine("Hit: " + hit.Uri);
}
}

static void OnFinished(FinishedResponse response)
{
    // the application is done, we can tell Gtk# to quit now
    Application.Quit();
}
```

When you're done, press F8 to compile your program. If you encounter any errors, you have typed something incorrectly, so check carefully against the preceding text. Now open a terminal, change to the directory where you created your project, then look inside there for the bin/Debug subdirectory. All being well, you should find the BeagleTest.exe file in there, which you can run like this:

```
mono BeagleTest.exe hello
```

If you get a long string of errors when you run your program, try running this command first: export MONO_PATH=/usr/lib/beagle. That tells Mono where to look for the Beagle library, which is probably your problem.

# Creating a GUI with Gtk#

Gtk# was included with Gnome by default for the first time in Gnome 2.16, but it had been used for a couple of years prior to that and so was already mature. MonoDevelop comes with its own GUI designer called Stetic, which lets you drag and drop GUI elements onto your windows to design them.

To get started, go to File, New Project in MonoDevelop, choose C#, then Gtk# 2.0 project. Call it GtkTest, and deselect the box asking MonoDevelop to make a separate directory for the solution. You'll find that Main.cs contains a little more code this time because it needs to create and run the Gtk# application. However, the actual code to create your GUI lives in User Interface in the left pane. If you open that group, you'll see MainWindow, which, when double-clicked, brings up MonoDevelop's GUI designer.