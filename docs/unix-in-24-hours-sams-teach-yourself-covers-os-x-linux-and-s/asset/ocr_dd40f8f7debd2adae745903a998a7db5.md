```
./Src/Misc/info.c
./Src/Misc/isnew.c
./Src/Misc/mydates.c
./Src/Misc/showmatches.c
./Src/Misc/change.c
./Src/change.c
./Src/cleanup.c
./Src/cribbage.c
./Src/expandurl.c
./Src/extract-mail.c
./Src/futuredate.c
./Src/import.c
./Src/assemble.c
./Src/make-html.c
./Src/old-import.c
./Src/process-data.c
./Src/showmatches.c
./Src/sum-up.c
./Src/text-counter.c
./Src/login.c
./Src/calc.c
$
```

In this case, the −i flag indicates that I want to have it read an existing archive, −t indicates that I only want a listing of the files, not to have them extracted, and −I lets me specify the input filename.

# 3. The easiest way to extract a file is to specify the pattern that should be compared.

Notice in this case that I’m going to feed the archive into cpio as standard input. It’s a common way to use the command:

Click here to view code image

```
$ cpio -i cribbage < sourcefile.cpio
cpio: WARNING! These patterns were not matched:
cribbage
$
```

Nope. The pattern cribbage didn’t work. In fact, it wasn’t a regular expression, so cpio helpfully indicated that there weren’t any matches. Here’s an improved attempt:

Click here to view code image

```
$ cpio -i "*cribbage*" < *cpio
cpio: Unable to create ./Src/cribbage.c <No such file or directory>
$
```

# 4. We’re almost there, but there’s still a problem, though the cpio error message isn’t too helpful in explaining what’s happening. The problem is that there is no Src directory, and the program can’t create subdirectories without a new flag, −d, being added. The error message is more confusing than informative of that fact, however.

While I’m at it, I’ll also add −v to ensure some verbose output as it unpacks:

Click here to view code image

```
$ cpio -ivd '*cribbage*' < *cpio
./Src/cribbage.c
30 blocks
$
```