# REASSEMBLING SPLIT FILES: cat

So what do you if you've got a bunch of split up files and want to put them back together? It's simple—remember the `cat` command? When you have a series of files named with something such as `<basename>` `<basename>aa`, `<basename>ab`, `<basename>ac`... `<basename>zz`, you can reassemble them by issuing the `cat` command as follows: `cat <basename>* > complete.file`. After `cat` has concatenated the files for you, you can `mv` the `complete.file` (or whatever you named it) to whatever final name you want.

![](bbox=[0.15, 0.44, 0.22, 0.55])

> **Working with Output Files** It's frequently best to call output files by names such as complete file—something completely different than the `<basename>`—and then move them to their destination or final filename. This avoids potential confusion in those cases where you really want your final filename to be just `<basename>`

# COMPARING AND REVISING FILES: diff AND patch

You might be accustomed to creating documents and sending out revisions. Unfortunately, most of the time you probably have to send out complete copies of files when only a few words here and there have changed. In the UNIX community, there is a great deal of information exchange, and source code is passed back and forth constantly. Rather than always sending complete files, people rely on the `diff` and `patch` commands to only transfer whatever information has changed between revisions.

# USING diff

The `diff` function takes two files—an original template file and an updated file—and produces an output `patchfile` that contains enough information to reconstruct the updated file given only the patchfile and the template file. Assume you have the original file `templatefile.txt`, which has the following contents: