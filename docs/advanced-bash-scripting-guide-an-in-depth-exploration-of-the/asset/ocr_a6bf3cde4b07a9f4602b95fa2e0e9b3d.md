# Advanced Bash-Scripting Guide

```
fi
done
```

```
# Don't need an "else" clause here,
#+ because Stupid Strategy will always fail and exit!
# For Moves in (1..63)
cposl=$1
moves=$( $(generate_moves $curpos))
do_move="$curpos"
if [ \$? -eq \$FAIL ];
then
    failure
fi
```

> # Could have condensed above two do-loops into a single one,
echo #+ but this would have slowed execution.

```
print_board
echo echo "Knight's Tour ends on $(to_algebraic $curpos) [square $curpos]."
return $SUCCESS
```

```
debug () {
    local n
    # Enable this by setting DEBUG=1 near beginning of script.
    echo "At move number $movenum:"
    echo "**** possible moves =Smp ****"
    echo ### square = $square ###"
    echo "lmin = $lmin"
    echo "${moves[$i]}"
}
```

```
for n in {1..8};
do
    echo "* $(n):$(p_moves[n])"
done
echo echo "iex $iex : mcves = ${moves[iex]}"
echo "square = \$square"
echo
```

> # Gives pretty complete status after ea. move.

```
# int main () {
from_algebraic "$1"
startpos=$$
if [ "$startpos" -eq \$FAIL ]; then
    # Okay even if no $1.
else
    echo "No starting square specified (or illegal input)."
    # even if input -lt 0.
    let startpos=\$RANDOM % $SQUARES # 0 - 63 permissible range.
fi
```

Appendix A. Contributed Scripts

739