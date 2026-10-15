```
```
$ ps -ef | head -5
USER PID %CPU %MEM SZ RSS TT STAT ENG TIME COMMAND
news 7460 97.7 0.4 336 252 ? R N 4 4:33 sort -u
→ /tmp/nnsubj6735a
phaedrus 8693 18.1 1.1 1260 720 rm S 0:03 nn
root 8741 14.4 0.4 416 252 ? R 9 0:03 nntpd
root 8696 13.9 0.4 416 252 ? S 0:03 nntpd
Broken pipe
$ kill 7460
7460: Not owner
$ 
```
```