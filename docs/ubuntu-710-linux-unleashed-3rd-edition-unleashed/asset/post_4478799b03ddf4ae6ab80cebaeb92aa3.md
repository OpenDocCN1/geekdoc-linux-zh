
// even more
} else {
    // only executed if none of the others are
}

## Building on Mono's libraries

Ubuntu ships with several Mono-built programs, including Tomboy and Beagle. It also comes with a fair collection of .NET-enabled libraries, some of which you probably already installed earlier. The nice thing about Mono is that it lets you build on these libraries really easily: You just import them with a using statement, then get started.

To demonstrate how easy it is to build more complicated Mono applications, we're going to produce two: one using Beagle, the super-fast file indexer, and one using Gtk#, the GUI toolkit that's fast becoming the standard for Gnome development. Each has its own API that takes some time to master fully, but you can get started with them in minutes.

## Searching with Beagle

Beagle is the de facto Linux search tool for Gnome, and is also used by several KDE-based programs. It works by scanning your computer in the background, then monitoring for file system changes so that its data always stays up to date. However, the magic is that it indexes data cleverly—if you tag your images, it reads those tags. If you have album and artist data in your MP3s, it reads that data too. It also reads your emails, your instant messenger conversations, your web browser history, and much more—and provides all this data in one place, so if you search for "firefox" you'll find the application itself, all the times you've mentioned Firefox in your emails, and so on.

In MonoDevelop, go to File, New Project, select C#, then choose Console Project. Give it the name BeagleTest, and tell MonoDevelop not to create a separate directory for the solution, and also that you don't want Gtk# support or Packaging Integration. You'll be back at the default Hello World program, but you're going to change that. First, you need to tell Mono that you want to use Beagle and Gtk# by hand, rather than using its project wizard. No, you're not going to create a GUI for your search, but you do want to take advantage of Gtk#'s idle loop system—we'll explain why soon.

To add references to these two libraries, right-click on the word References in the left pane (just above Resources) and select Edit References. A new window appears (shown in Figure 27.3), and from that you should make sure Beagle and gtk-sharp are selected. Now click OK, and the References group on the left should expand so that you can see you have Beagle, gtk-sharp, and System (the last one is the default reference for .NET programs).

Now it's time to write the code. At the top of the Main.cs file (your main code file), you need to edit the "using" statements to look like this:

```
using System;
using System.Collections;
using Beagle;
using Gtk;
```

![](img/7aaa8e4f2209bf9f2fb443905096e94c_646_0.png)

**FIGURE 27.3** You need to tell Mono exactly which resource libraries you want to import for your program.

The BeagleTest namespace and MainClass class aren’t changing, but you do need to edit the `Main()` method so that you can run your Beagle query. Here’s how it should look, with C# comments (//, as in C++) sprinkled throughout to help you understand what’s going on:

```
public static void Main(string[] args)
{
    Application.Init();

    // "Query" is the main Beagle search type.
    //It does lots of magic for you - you just need to provide it with a search
term and tell it where to search
    Query q = new Query();

    // these two are callback functions.
    // What you're saying is, when a hit is returned
    // (that is, when Beagle finds something, it should
    // run your OnHitsAdded() method. That code isn't written
    // yet, but you'll get there soon.
    q.HitsAddedEvent += OnHitsAdded;
    q.FinishedEvent += OnFinished;

    // these two tell Beagle where to search
    q.AddDomain(QueryDomain.Neighborhood);
    q.AddDomain(QueryDomain.Global);
```

```
// finally, you tell Beagle to search for the first word
// provided to your command (args[0]), then ask it
// to asynchronously run its search. That is, it runs
// in the background and lets your program continue running
q.AddText(args[0]);
q.SendAsync();

// tell Gtk# to run
Application.Run();
}
```

The only thing I haven’t explained in there is the Gtk# stuff, but you might already have guessed why it’s needed. The problem is this: Beagle runs its search asynchronously, which means that it returns control to your program straight away. Without the Application.Run() call, the SendAsync() method is the last thing your program does, which meant that it terminates itself before Beagle actually has chance to return any data. So, Gtk# serves as an idle loop: when you call Run(), Gtk# makes sure your program carries on running until you tell it to quit, giving Beagle enough time to return its results.

Now, let’s take a look at the OnHitsAdded and OnFinished methods, called whenever Beagle finds something to return and when it’s finished searching, respectively:

```
static void OnHitsAdded (HitsAddedResponse response)
{
    // sometimes Beagle can return multiple hits (files)
    // in each response, so you need to go through each
    // one and print it out line by line
    foreach(Hit hit in response.Hits)
    {
        // the Uri of hits is its location, which might
        // be on the web, on your filesystem, or somewhere else
        Console.WriteLine("Hit: " + hit.Uri);
    }
}
```

```
static void OnFinished(FinishedResponse response)
{
    // the application is done, we can tell Gtk# to quit now
    Application.Quit();
}
```

When you’re done, press F8 to compile your program. If you encounter any errors, you have typed something incorrectly, so check carefully against the preceding text. Now open a terminal, change to the directory where you created your project, then look inside
