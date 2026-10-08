# Advanced Bash-Scripting Guide

```
# Set variable to pass as parameter to "display" function.
avar=$(echo "${array[@]}") # Convert array to string variable.
display="$avar" # Display it.
echo;
echo "Generation $generation    $alive alive"
```

```
if [ "$alive" -eq 0 ];
then
    echo
    echo "Premature exit: no more cells alive!"
    exit $NONE_ALIVE    # No point in continuing
                      # if no live cells.
fi
```

```
# main ()
{
    # Load initial array with contents of startup file.
    initial=$(cat "$startfile" | sed -e '/#/d' | tr -d '\n')
    # Delete lines containing # comment character.
    sed -e 's/\\//g' -e 's/\_/g'
    # Remove linefeeds and insert space between elements.
```

```
clear
echo # Title
setterm -reverse off
echo "$GENERATIONS generations"
echo "$of"
echo "*Life in the Slow Lane\*"
setterm -reverse on
```

```
setterm -reverse off
sleep $DELAY # Display "splash screen" for 2 seconds.
```

```
# Display first generation.
Gen0=$(echo "${initial[0]}\'
display="$Gen0" # Display only.
echo;echo
echo "Generation $generation    $alive alive"
sleep $DELAY
```

```
let generation += 1 # Bump generation count.
echo
```

```
# Display second generation.
Cur=$(echo "${initial[0]}\'
next_gen="$Cur" # Update & display.
sleep $DELAY
```

Appendix A. Contributed Scripts

593