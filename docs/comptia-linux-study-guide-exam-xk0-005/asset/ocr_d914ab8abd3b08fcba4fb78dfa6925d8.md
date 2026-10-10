```
$ cp Emphasis Story-Line
cp: omitting directory 'Emphasis'
$
$ ls -F
Emphasis/
$
$ cp -R Emphasis Story-Line
$
$ ls -F
Emphasis/  Story-Line/
$
$ ls -R Emphasis
Emphasis:
chivalric-romance.txt      melodrama.txt
interplanetary-battles.txt space-warfare.txt
$
$ ls -R Story-Line/
Story-Line/:
chivalric-romance.txt      melodrama.txt
interplanetary-battles.txt space-warfare.txt
$
```

Note that the first time the cp command is used in Listing 3.8, the -R option is not used, and thus the source directory is not copied. The error message generated, `cp: omitting directory`, can be a little confusing, but essentially it is telling you that the copy will not take place. When the cp -R command is used to copy the source directory in Listing 3.8, it is successful. The recursive copy option is one of the few command options that can be uppercase, -R, or lowercase, -r.

To move or rename a file or directory locally, you use a single command: mv. The command's basic syntax is nearly the same as the cp command:

```
mv [OPTION]... SOURCE DEST
```

The commonly used mv command options are similar to cp command options. However, you'll notice in Table 3.3 that there are fewer typical mv command options than common cp options. As always, be sure to view the mv utility's man pages, using the man mv command, to review all the options for certification studying purposes and explore uncommon options, which may be useful to you.

The move command is simple to use. A few examples of renaming a file as well as employing the -i option to avoid renaming a file to a preexisting file are shown in Listing 3.9.