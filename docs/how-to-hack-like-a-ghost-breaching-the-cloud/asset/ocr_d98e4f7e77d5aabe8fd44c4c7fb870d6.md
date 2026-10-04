```
"Key": "Archive/_old",
"LastModified": "2015-04-08T22:01:48.000Z",
"Size": 2969,

"Key": "index.html",
"LastModified": "2015-04-08T22:01:49.000Z",
"Size": 0,
},
--snip--
```

We get a lot of objects—too many to manually inspect. To find out exactly how many, we grep the "Key" parameters:

```
root@Point1:~# grep '"Key"' list_objects.txt | wc -l
425927
```

Bingo! We have more than 400,000 files stored in this single bucket. That's as good a catch as they come. In the list of objects, note the empty index.html at the root of the S3 bucket; an S3 bucket can be set up to act as a website hosting static files like JavaScript code, images, and HTML, and this index.html file is what's responsible for the blank page we got earlier when running the URL.

# S3 FILING SYSTEM

Also notice how S3’s internal catalog system lacks any hierarchical order. It’s a common misconception to think of S3 as a filesystem. It’s not. There are no folders, or indeed files—at least not in their common modern definitions. S3 is a key-value storage system. Period. AWS’s web console gives the illusion of organizing files inside folders, but that’s just some GUI voodoo. A folder in S3 is simply a key pointing to a null value. A file that seems to be inside a folder is nothing more than a blob of storage referenced by a key named like /folder/file. As another way to put it, using the AWS CLI, we can delete a folder without deleting that folder’s files because the two are absolutely not related.

It’s time for some poor man’s data mining. Let’s use regex patterns to look up SQL scripts, bash files, backup archives, JavaScript files, config files, VirtualBox snapshots—anything that might give us valuable credentials:

```
# We extract the filenames in the "Key" parameters:
root@Point1:~# grep '"Key"' list_objects | sed 's/[" ,]/ /g' > list_keys.txt

root@Point1:~# patterns='\.sh$|\.sql$|\.tar\.gz$|\.properties$|\.config$|\.tgz$'

root@Point1:~# egrep $patterns list_keys.txt
Key: debug/360-ios-safari/deploy.sh
```