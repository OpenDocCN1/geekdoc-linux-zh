```
```
du -sh reports/*
4.7G  reports/
$ 
```
```

# Reuse the Nth Word from a Previous Command

```
```
$ !!!:N
$ <event_designator>:<number>
```
```

To access a word in the previous command use `!!:N` where N is the number of the word you wish to retrieve. The first word is 0, the second word is 1, etc. You can think of 0 as being the command, 1 as being the first argument to the command, 2 as being the second argument, and so on.

You can use any event designator in conjunction with a word designator. In the following example, `!!` is the most recent command line: `avconv -i screencast.mp4 podcast.mp3`. The `!a` event designator expands to that same command since it’s the most recent command that started with the letter “a.”

```
```
$ avconv -i screencast.mp4 podcast.mp3
$ mv !!:2 converted/
mv screencast.mp4 converted/
$ mv !a:3 podcasts/
mv podcast.mp3 podcasts/
$ 
```
```

# Repeat the Previous Command While Substituting a String

```
```
$ ^<string1>^<string2>^
```
```

This little trick is great for quickly correcting typing mistakes. If you omit `^<string2>^`, then `<string1>` will be removed from the previous command. By