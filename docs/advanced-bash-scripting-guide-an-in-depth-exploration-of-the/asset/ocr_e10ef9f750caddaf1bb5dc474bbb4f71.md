# Advanced Bash-Scripting Guide

```
let $basewidth = $MWIDTH + $SMARGIN
# "Base" beneath rods.
# Above "algorithm" could likely stand improvement.
```

```
let lastmove_t = $DISKS - 1

# Final move?
```

```
declare -a Rod1 Rod2 Rod3

### ################################
```

```
function repeat { #1-char $2-number of repetitions
  local n
  # Repeat-print a character.
  for (( n=0; n<$2; n++ )); do
    echo -n "$1"
  do
}
```

```
function FromRod {
  local rod summit weight sequence
  while true; 
    do
      rod=$(rod/[^123]/) || continue
      sequence=$(echo $(seq 0 $disks1 | tac))
      for summit in $sequence; do
        eval weight=\$(Rod($rod)[summit])
        test $weight -ne 0 && \
          echo "$rod $summit $weight"; return;
      done
    done
}
```

```
function ToRod { # $1-previous (FromRod) weight
  local rod firstfree sequence
  while true; 
    do
      rod=$(rod/[^123]) || continue
      sequence=$(echo $(seq 0 $disks1 | tac))
      for firstfree in $sequence; do
        eval weight=\$(Rod($rod)[$firstfree])
        test $weight -gt 0 && (( (firstfree++ )); break;
      done
      test $weight -gt $1 -o firstfree = 0 && \
        echo "$rod $firstfree"; return;
    do
}
```

```
function PrintRods {
  local disk empty fill sp sequence
```

Appendix A. Contributed Scripts