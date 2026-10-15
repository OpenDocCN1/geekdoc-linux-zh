
Fortunately, the Unix rule for hiding files is much easier than that for either the Mac or PC. No secret status flag reminds the system not to display the file when listing directories. Instead, the rule is simple: Any filename that starts with a dot (.) is a hidden file.

## Note

> A hidden file is any file with a dot as the first character of the filename.

If the filename or directory name begins with a dot, it won’t show up in normal listings of that directory. If the filename or directory name has any other character as the first character of the name, it lists normally.

- 1. Turn to your computer and enter the ls command to list all the files and directories in your home directory:

Click here to view code image

```
% ls -F
Archives/      Mail/          RUMORS.18Sept  mailing.lists
InfoWorld/     News/          bin/           newlists
LISTS          OWL/           iecc.list      src/
%
```

You can see that I have 12 items in my own directory, 7 directories (the directory names have a slash as the last character because of the -F, remember), and 5 files. Files have minimal rules for naming, too. Avoid slashes, spaces, and tabs, and you’ll be fine.

- 2. Without an explicit direction to the contrary, Unix is going to let the hidden files remain hidden. To add the hidden files to the listing, you just need to add a -a flag to the command. Turn to your computer and try the ls -aF command to see what hidden files are present in your directory. These are my results:

Click here to view code image

```
% ls -aF
./             .gopherrc      .oldnewsrc     .sig           RUMORS.18Sep
../            .history*      .plan          Archives/      bin/
.A genda       .info          .pnewsexpert   InfoWorld/     iecc.list
.aconfigrc     .letter        .report        LISTS          mailing.lists
.article       .login         .rm-timestamp  Mail/          newlists
.cshrc         .mailrc        .rnlast        News/          src/
.elm/          .newsrc        .rnsoft        OWL/
%
```

Many dot files tend to follow the format of a dot, followed by the name of the program that owns the file, with rc as the suffix. In my directory, you can see six dot files that follow this convention: .aconfigrc, .cshrc, .gopherrc, .mailrc, .newsrc, and .oldnewsrc.

Because of the particular rules of hidden files in Unix, they are often called dot files, and you can see that I have 23 dot files and directories in my directory.

## Note

The rc suffix (meaning “resource config”) tells you that this file is a configuration file for a particular utility. For instance, .cshrc is the configuration file for the C shell and is executed every time the C shell (/bin/csh) is executed. You can define aliases for C shell commands and a special search path, for example.

## Note

Because it’s important to convey the specific filename of a dot file, pronunciation is a little different from elsewhere in Unix. The name .lynxrc would be spoken as “dot-lynx-are-sea,” and .mailrc would be “dot mail are sea.” If you can’t pronounce the program name, odds are good that no one else can either, so .cshrc is “dot-sea-ess-aitch-are-sea.”

Other programs create many different dot files and try to retain a consistent naming scheme. You can see that .rnlast and .rnsoft are both from the rn program, but it’s difficult to know simply from the filenames that .article, .letter, .newsrc, .oldnewsrc, and .pnewsexpert are all also referenced by the rn program. Recognizing this problem, some application authors designed their applications to create a dot directory, with all preference files neatly tucked into that one spot. The elm program does that with its .elm hidden directory.

Some files are directly named after the programs that use them: The .Agenda file is used by the agenda program, and .info is used by the info program. Those almost have a rule of their own, but it’s impossible to distinguish them from .login, from the sh program; .plan for the finger program; .rm-timestamp from a custom program of my own; and I frankly have no idea what program created the .report file!

This should give you an idea of the various ways that Unix programs name and use hidden files. As an exercise, list all the dot files in your home directory and try to figure out which program created each file. Check by looking in the index of this book to see whether a program by that name exists, if it’s a .xxx file. If you can’t figure out which programs created which files, you’re not alone. Keep the list handy; refer to it as you learn more about Unix while exploring this book, and by the time you’re done, you’ll know exactly how to find out which programs created which dot files.

## Task 3.3: The Special Directories . and ..

I haven’t mentioned two dot directories, although they show up in my listing and most certainly show up in your listing, too. They are dot and dot-dot (. and ..), and they’re shorthand directory names that can be terrifically convenient.

The dot directory is shorthand for the current location in the directory hierarchy; the dot-dot directory moves you up one level, to the parent directory.

Consider again the list of files shown in Figure 3.3. If you were looking at the files in the
