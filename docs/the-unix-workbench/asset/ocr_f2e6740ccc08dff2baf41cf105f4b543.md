```
ls
```

+   Code
+   Documents
+   Photos
+   Desktop
+   Music
+   echo-out.txt
+   journal-2017-01-24.txt
+   todo.txt

It’s gotten a little sloppy, so let’s clean this directory up. First I want to make a new directory to store all of my journal entries in called Journal. We already know how to do that:

```
mkdir Journal
```

Now I want to move my journal entry journal-2017-01-24.txt into the Journal directory. We can move it using the mv command. mv takes two arguments: first the path to the file or folder that you wish to move followed by the destination folder. Let’s try using mv now:

```
mv journal-2017-01-24.txt Journal
ls
```