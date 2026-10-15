If you come from the Windows world, you may be accustomed to a file’s extension indicating what type of file it is and whether it can be executed. In UNIX and Linux, the file permission bits indicate whether a file can be executed, and if so, by whom. If you wish, you can give your bash scripts a **.sh** suffix to remind you what they are, but you’ll then have to type out the **.sh** when you run the command, since UNIX doesn’t treat extensions specially.

# From commands to scripts

Before we jump into bash’s scripting features, a note about methodology. Most people write bash scripts the same way they write Perl or Python scripts: with a text editor. However, it’s more productive to think of your regular shell command prompt as an interactive script development environment.

For example, suppose you have log files named with the suffixes **.log** and **.LOG** scattered throughout a directory hierarchy and that you want to change them all to the uppercase form. First, let’s see if we can find all the files.

```
```bash
$ find . -name '*.log'
.do-not-touch/important.log
admin.com-log/
foo.log
genius/spew.log
leather.flog
...
```
```

Oops, it looks like we need to include the dot in our pattern and to leave out directories as well. Type <Control-P> to recall the command and then modify it.

```
```bash
$ find . -type f -name '*.log'
.do-not-touch/important.log
foo.log
genius/spew.log
...
```
```

OK, this looks better. That **.do-not-touch** directory looks dangerous, though; we probably shouldn’t mess around in there.

```
```bash
$ find . -type f -name '*.log' | grep -v .do-not-touch
foo.log
genius/spew.log
...
```
```

All right, that’s the exact list of files that need renaming. Let’s try generating some new names.

```
```bash
$ find . -type f -name '*.log' | grep -v .do-not-touch | while read fname
> do
> echo mv $fname ${fname/.log/.LOG/}
> done
mv foo.log foo.LOG
mv genius/spew.log genius/spew.LOG
...
```
```