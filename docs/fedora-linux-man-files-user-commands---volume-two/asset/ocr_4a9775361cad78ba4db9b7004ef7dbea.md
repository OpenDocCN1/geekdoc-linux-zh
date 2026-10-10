# EXAMPLE

Given a commit, find out where it is relative to the local refs. Say somebody wrote you about that fantastic commit 33db5f4d9027a10e477ccf054b2c1ab94f74c85a. Of course, you look into the commit, but that only tells you what happened, but not the context.

Enter `git name-rev`:

```
```
% git name-rev 33db5f4d9027a10e477ccf054b2c1ab94f74c85a
33db5f4d9027a10e477ccf054b2c1ab94f74c85a tags/v0.99~940
```
```

Now you are wiser, because you know that it happened 940 revisions before v0.99. Another nice thing you can do is:

```
```
% git log | git name-rev --stdin
```
```