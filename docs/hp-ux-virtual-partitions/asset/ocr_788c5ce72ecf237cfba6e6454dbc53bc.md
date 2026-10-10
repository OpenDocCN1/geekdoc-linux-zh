```
```bash
# cd /var/tmp
# ls -1 aa*
-rw-rw-rw- 1 root sys      102 Jul 11 15:20 aaaa01112
-rw-rw-rw- 1 root sys      102 Jul 11 15:37 aaaa01299
-rw-rw-rw- 1 root sys      102 Jul 11 15:37 aaaa01333
-rw-rw-rw- 1 root sys      102 Jul 11 15:38 aaaa01354
-rw-rw-rw- 1 root sys       99 Jul 11 15:40 aaaa01380
-rw-rw-rw- 1 root sys       99 Jul 11 15:40 aaaa01405
-rw-rw-rw- 1 root sys      102 Jul 11 15:47 aaaa01426
-rw-rw-rw- 1 root sys       99 Jul 11 15:45 aaaa01487
-rw-rw-rw- 1 root sys      102 Jul 11 14:24 aaaa01558
# rm aaaa01487
# cd /
# frecover -x -i /var/tmp/aaaa01487 -f /dev/rmt/0m
# cd /var/tmp
# ls -1 aa*
-rw-rw-rw- 1 root sys      102 Jul 11 15:20 aaaa01112
-rw-rw-rw- 1 root sys      102 Jul 11 15:37 aaaa01299
-rw-rw-rw- 1 root sys      102 Jul 11 15:37 aaaa01333
-rw-rw-rw- 1 root sys      102 Jul 11 15:38 aaaa01354
-rw-rw-rw- 1 root sys       99 Jul 11 15:40 aaaa01380
-rw-rw-rw- 1 root sys       99 Jul 11 15:40 aaaa01405
-rw-rw-rw- 1 root sys      102 Jul 11 15:47 aaaa01426
-rw-rw-rw- 1 root sys       99 Jul 11 15:45 aaaa01487
-rw-rw-rw- 1 root sys      102 Jul 11 14:24 aaaa01558
# ```
```

In the previous example, we successfully restored the file /var/tmp/aaaa01487 from the tape using frestore.

There are some powerful aspects to backup that we did not employ in our example. These include backup levels, graph files, and index files. backup supports backup levels 0-9, 0 is used for full backups and the other digits indicate various incremental backup levels.

Graph files are used to specify the files to be included in the backup. Index files contain a list of files produced as part of the backup. Let's take a look at an example that employs all of these functions. First, we create a graph file that contains the files we wish to include (i) or exclude (e) as part of the backup. In our case the file will contain only the following line:

```
```text
i /var/tmp
```
```

Let's now run fbackup with u to update the backup database, O for a full backup, f to specify the file to which we want to write the backup (we'll use a file rather than tape in this example), g to specify our graph file, I to specify the name of the index file, and finally, we'll redirect messages to a