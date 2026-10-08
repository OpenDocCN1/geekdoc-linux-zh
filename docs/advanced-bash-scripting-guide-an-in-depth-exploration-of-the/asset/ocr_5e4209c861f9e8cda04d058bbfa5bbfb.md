# Advanced Bash-Scripting Guide

```
####################
# Constants #
SQUARES=16 #
FAIL=70 #
E_PREMATURE_EXIT=80 #
####################
```

```
########
# Data #
########
Puzzle={ 1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 " " }
```

```
####################
# Functions #
################
```

```
function swap
{
local tmp

tmp=${Puzzle[$1]}
Puzzle[$1]=${Puzzle[$2]}
Puzzle[$2]=$tmp
}
```

```
function Jumbo
{ # Scramble the pieces at beginning of round.
local i pos1 pos2

for i in {1..100}
do
pos1=$(( ($RANDOM % $SQUARES ))
pos2=$(( ($RANDOM % $SQUARES ))
swap $pos1 $pos2
done
```

```
function PrintPuzzle
{
local il i2 puzpos
puzpos=0
```

```
clear
echo "Enter quit to exit."; echo # Better than Ctrl-C.

echo "","------" # Top border.
for il in {1..4}
do
for i2 in {1..4}
do
printf "|%2s "${Puzzle[$puzpos]}"
((puzpos++))
done
echo "|"" # Right-side border.
test $il - 4 || echo "--------------------"
```

Appendix A. Contributed Scripts

743