# ## BATCH MODE

Batch mode can be used to apply the sa set of updates to many identical systems. Suppose one has a tree which is replicated on a nuer of hosts. Now suppose so changes have been made to this source tree and those changes need to be propagated to the other hosts. In order to do this using batch mode, rsync is run with the write-batch option to apply the changes made to the source tree to one of the destination trees. The write-batch option causes the rsync client to store in a “batch file” all the information needed to repeat this operation against other, identical destination trees.

Generating the batch file once saves having to perform the file status, checksum, and data block generation more than once when updating multiple destination trees. Multicast transport protocols can be used to transfer the batch update files in parallel to many hosts at once, instead of sending the sa data to every host individually.

To apply the recorded changes to another destination tree, run rsync with the read-batch option, specifying the na of the sa batch file, and the destination tree. Rsync updates the destination tree using the information stored in the batch file.

For your convenience, a script file is also created when the write-batch option is used: it will be nad the sa as the batch file with “.sh” appended. This script file contains a command-line suitable for updating a destination tree using the associated batch file. It can be executed using a Bourne (or Bourne-like) shell, optionally passing in an alternate destination tree pathna which is then used instead of the original destination path. This is useful when the destination tree path on the current host differs from the one used to create the batch file.

Examples:

```
```
$ rsync --write-batch=foo -a host:/source/dir/ /adest/dir/ $ scp foo* remote: $ ssh remote ./foo.sh /bdest/dir/
```
```

```
```
$ rsync --write-batch=foo -a /source/dir/ /adest/dir/ $ ssh remote rsync --read-batch= -a /bdest/dir/ <foo
```
```

In these examples, rsync is used to update /adest/dir/ from /source/dir/ and the information to repeat this operation is stored in “foo” and “foo.sh”. The host “remote” is then updated with the batched data going into the directory /bdest/dir. The differences between the two examples reveals so of the flexibility you have in how you deal with batches:

+   *   The first example shows that the initial copy doesn’t have to be local — you can push or pull data to/from a remote host using either the remote-shell syntax or rsync daemon syntax, as desired.

+   *   The first example uses the created “foo.sh” file to get the right rsync options when running the read-batch command on the remote host.