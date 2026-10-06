# Advanced Bash-Scripting Guide

```
then
    # If alive, then
    array[$si]=.
    # represent the cell as a period.
else
    array[$si]=""
    # Otherwise underscore
    # (which will later be converted to space)
fi
    let i += 1
done
```

```
# let "generation += 1"    # Increment generation count
# Set variable to pass as parameter to "display" function.
avavar="${array[@]}" # Convert array back to string variable.
display "$avar"\      # Display it.
echo; echo
echo "Generation $generation --$alive"
```

```
if [ "$alive" -eq 0 ];
then
    echo
    echo "Premature exit: no more cells alive!"
    exit NON_ALIVE    # No point in continuing
fi
    # if no live cells.
```

```
}
```

```
====================================================
```

```
# main()
```

```
# Load initial array with contents of startup file.
initial=$(cat "$startfile" | sed -e '#/.*d' | tr -d '\n' \
sed -e 's/\/./g' -e 's/_/g')
# Delete lines containing #1 comment character.
# Remove linefeeds and insert space between elements.
```

```
clear
    # Clear screen.
```

```
echo #    Title
echo "========================"
echo "    $GENERATIONS generations"
echo "        of"
echo "\"Life in the Slow Lane\"
echo "========================"
```

```
-------- Display first generation. --------
Gen0="${initial[0]}"
display "$Gen0"      # Display only.
echo; echo
echo "Generation $generation --$alive"
--------------------------------
```

```
let "generation += 1"    # Increment generation count.
echo
-------- Display second generation. --------
Cur="${initial[@]}"
next_gen="$Cur"\      # Update & display.
--------------------------------
```

Appendix A. Contributed Scripts