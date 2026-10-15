# EXAMPLE 6.4

```
1 % df | nawk '$4 > 75000'
/oracle (/dev/dsk/c0t0d0s7):399780 blocks 105756 files
/opt (/dev/dsk/c0t0d0s8):1943994 blocks 49187 files
```

```
2 % rusers | nawk '/root$/ {print $1}'
owl
crow
bluebird
```

# EXPLANATION

+   1 The df command reports the free disk space on file systems. The output of the df command is piped to nawk. If the fourth field is greater than 75,000 blocks, the line is printed.
+   2 The rusers command prints those logged on remote machines on the network. The output of the rusers command is piped to nawk as input. The first field is printed if the regular expression root is matched at the end of the line ($); that is, all machine names are printed where root is logged on.

# 6.3 How awk Works

Before getting into all the details of awk, let's look at how it does its job, step by step. We'll look at a simple three-line file called names:

```
Tom Savage 100
Molly Lee 200
John Doe 300
```

The awk command follows:

```
% nawk '{print $1, $3}' names
```

+   1. Awk takes a line of input (from a file or pipe) and puts the line into an internal variable called $0. Each line is also called a record and is terminated by a new-line, by default.

![](bbox=[0.25, 0.85, 0.65, 0.95])

+   2. Next, the line is broken into fields (words) separated by whitespace. Each field is stored in a numbered variable, starting with $1. There can be as many as 100 fields.