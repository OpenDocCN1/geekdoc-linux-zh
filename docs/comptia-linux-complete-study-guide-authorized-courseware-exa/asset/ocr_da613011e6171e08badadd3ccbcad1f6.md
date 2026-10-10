**Display process hierarchy** The `-H, -f,` and `--forest` options group processes and use indentation to show the hierarchy of relationships between processes. These options are useful if you’re trying to trace the parentage of a process.

**Display wide output** The `ps` command output can be more than 80 columns wide. Normally, `ps` truncates its output so that it will fit on your screen or `xterm`. The `-w` and `w` options tell `ps` not to do this, which can be useful if you direct the output to a file, as in `ps w > ps.txt`. You can then examine the output file in a text editor that supports wide lines.

You can combine these `ps` options in many ways to produce the output you want. You’ll probably need to experiment to learn which options produce the desired results because each option modifies the output in some way. Even those that would seem to influence just the selection of processes to list sometimes modify the information that’s provided about each process.

# # Interpreting ps Output

Listings 2.3 and 2.4 show a couple of examples of `ps` in action. Listing 2.3 shows `ps -u roedsmith --forest`, and Listing 2.4 shows `ps u U roedsmith`.

# **Listing 2.4:** Output of `ps -u roedsmith --forest`

```
$ ps -u roedsmith --forest

  PID TTY      TIME CMD
2451 pts/3  00:00:00 bash
2551 pts/3  00:00:00 ps
2496 ?      00:00:00 kvt
2498 pts/1  00:00:00 bash
2505 pts/1  00:00:00  \_ ndit
2506 ?      00:00:00  \_ csh
2544 ?      00:00:00    \_ eyeyes
19221 ?     00:00:01 dfm
```

# **Listing 2.5:** Output of `ps u U roedsmith`

```
$ ps u U roedsmith

USER     PID %CPU %MEM   VSZ  RSS TTY      STAT START TIME COMMAND
roedsmith 19221 0.0  0.5 4484 1984 ?     S  May 07  0:01 dfm
roedsmith  2451 0.0  0.8 1856 1048 pts/3  S  16:13  0:00 -bash
roedsmith  2496 0.2  3.2 6232 4124 ?     S  16:17  0:00 /opt/kd
roedsmith  2498 0.0  0.8 1860 1044 pts/1 S  16:17  0:00 bash
roedsmith  2505 0.1  2.6 4784 3332 pts/1 S  16:17  0:00 ndit
roedsmith  2506 0.0  0.7 2124 1012 ?     S  16:17  0:00 /bin/cs
roedsmith  2544 0.0  1.0 2576 1360 ?     S  16:17  0:00 eyeyes
roedsmith  2556 0.0  0.7 2588  916 pts/3 R  16:18  0:00 ps u U
```