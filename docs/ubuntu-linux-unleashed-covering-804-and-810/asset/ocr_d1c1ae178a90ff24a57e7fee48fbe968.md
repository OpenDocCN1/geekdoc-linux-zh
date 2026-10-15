```
// "Query" is the main Beagle search type.
// It does lots of magic for you - you just need to provide it with a search
// term and tell it where to search
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

The only thing I haven't explained in there is the Gtk# stuff, but you might already have guessed why it's needed. The problem is this: Beagle runs its search asynchronously, which means that it returns control to your program straight away. Without the Application.Run() call, the SendAsync() method is the last thing your program does, which meant that it terminates itself before Beagle actually has chance to return any data. So, Gtk# serves as an idle loop: when you call Run(), Gtk# makes sure your program carries on running until you tell it to quit, giving Beagle enough time to return its results.

Now, let's take a look at the OnHitsAdded and OnFinished methods, called whenever Beagle finds something to return and when it's finished searching, respectively:

```
static void OnHitsAdded (HitsAddedResponse response)
{
    // sometimes Beagle can return multiple hits (files)
    // in each response, so you need to go through each
    // one and print it out line by line
    foreach(Hit hit in response.Hits)
    {
```