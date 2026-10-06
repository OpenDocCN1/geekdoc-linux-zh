# Advanced Bash–Scripting Guide

```
row=$ $row * $ROWS
let $left = $row + $COLS # Left limit.
let $right = $left + $COLS - 1 # Right limit.

if [ "$1" -lt "$left" -o "$1" -gt "$right" ]
then
    return $FALSE # Beyond row boundary.
fi

return $TRUE # Valid coordinate.
}
nIsAlive () # Test whether cell is alive.
{
    # Takes array, cell number, state of cell as arguments.
    GetCount "$1" $2 # Get alive cell count in neighborhood.
    local nhbd=$

    if [ "$nhbd" -eq "$BIRTH" ] # Alive in any case.
then
        return $ALIVE
    fi

    if [ "$3" = "." -a "$nhbd" -eq "$SURVIVE" ]
then
        return $ALIVE # Alive only if previously alive.
    fi

    return $DEAD # Default.
}

Count () # Count live cells in passed cell's neighborhood.
{
    # Two arguments
    # $1 variable holding array
    # $2) cell number
    local cell_number=$2
    local array
    local top
    local center
    local bottom
    local r
    local row
    local i
    local t_top
    local t_cen
    local t_bot
    local count=0
    local ROW_NHBD=3

    array=( `echo "$1"` )

    let $top = $cell_number - $COLS - 1 # Set up cell number.
    let $center = $cell_number - 1
    let $bottom = $cell_number + $COLS - 1
    let $r = $cell_number / $ROWS
```

Appendix A. Contributed Scripts