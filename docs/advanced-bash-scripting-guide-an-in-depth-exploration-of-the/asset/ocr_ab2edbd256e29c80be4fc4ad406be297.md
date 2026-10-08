# Advanced Bash-Scripting Guide

```
echo "----'----'--------" # Bottom border.
}
```

```
function GetNum
  # Test for valid input.
  local pnum garbage
```

```
while true
do
  echo "$Moves: $moves" # Also counts invalid garbage
  read -p "Number to move: " pnum
  if [ "$pnum" = "quit" ]; then echo; exit $_PREMATURE_EXIT; fi
  test -z "$pnum" -n "${pnum//[0-9]/}" && continue
  test pnum -gt 0 -a pnum -lt $SQUARES && break
done
return $pnum
```

```
function GetPosFromNum
  # $1 = puzzle-number
  local juzpos
```

```
for juzpos in (0..14)
do
  test "${puzpos[$puzpos]}" = "$1" && break
done
return $puzpos
```

```
function Move
  # $1-Puzzle-pos
  test -gt 3 && test "${Puzzle[$((1 - 4))]}" = "\"
  && swap $1 ${{ $1 - 4 )) && return 0
  test $(( $1 % 4 )) -ne 3 && test "${Puzzle[$(($1 + 1))]}" = "\"
  && swap $1 ${{ $1 + 1 )) && return 0
  test -lt 12 && test "${Puzzle[$((1 + 4))]}" = "\"
  && swap $1 ${{ $1 + 4 )) && return 0
  test $(( $1 % 4 )) -ne 0 && test "${Puzzle[$(($1 - 1))))]}" = "\"
  && swap $1 ${{ $1 - 1 )) && return 0
return 1
```

```
function Solved
  local pos

  for pos in (0..14)
do
    test "${Puzzle[$pos]}" = ${{ $pos + 1 )) || return $FAIL
    # Check whether number in each square = square number.
done
return 0 # Success solution.
```

```
#################### MAIN () ####################
moves=0
jumble
```

Appendix A. Contributed Scripts