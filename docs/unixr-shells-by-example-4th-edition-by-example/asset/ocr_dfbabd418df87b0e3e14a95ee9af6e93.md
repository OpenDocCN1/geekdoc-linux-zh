# EXAMPLE 13.30 (CONTINUED)

```
2 $ fc -l -3
19      cd
20      history
21      fc -l
3 $ fc -ln
exit
history
ls
pwd
clear
cal 2000
history
vi file
history
ls -l
date
more file
echo a b c d
cd
history
fc -l
fc -l -3
4 $ fc -ln -3 > saved
5 $ more saved
fc -l
fc -l -3
fc -ln
6 $ fc -l 15
15      ls -l
16      date
17      more file
18      echo a b c d
19      cd
20      history
21      fc -l
22      fc -l -3
23      fc -ln
24      fc -ln -3 > saved
25      more saved
26      history
7 $ fc -l 15 20
15      ls -l
16      date
17      more file
18      echo a b c d
19      cd
20      history
```