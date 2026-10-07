# The Concurrent Versions System (CVS) 151

![](bbox=[0.049, 0.087, 0.595, 0.355])

Figure 7.0 Checking your environment variables

# Checking Files In

Now that you have created the CVS repository, you will probably want to check some files into it. CVS works differently than RCS in this regard. With CVS, you have the option of checking in (or out) entire filesystems (directory structures) or simply individual files.

Change directories to the directory that contains the files you want to commit to the CVS repository. For the sake of this example, you will say that the directory is the /Writing directory in your Home directory.

```
cd Writing
```

Now that you're in the directory, make sure that all the files you want to import are in the directory. Now you import the files from this directory into CVS.

```
cvs -d /mnt/cvsroot import -m 'New Example Files' sample Kara A2
```

It probably looks like a bit going on there, so break it into its component parts. Remember that you're really running two commands here—one that starts CVS and that is the actual CVS command you want to use.

The -d flag tells CVS which directory to use as the CVS root, and the following directory (/mnt/cvsroot) is the directory for this example. If you don't want to type this all the time, you can set your CVSROOT environment variable to