# Advanced Bash–Scripting Guide

```
echo

choice_of()
{
  select vegetable
  # [in list] omitted, so 'select' uses arguments passed to function.
  do
    echo "Your favorite veggie is $vegetable"
    echo "Yuck!"
    echo
    break
  done
}
choice_of beans rice carrots radishes tomatoes spinach
#  $1 $2 $3 $4 $5 $6
#  passed to choice_of() function

exit 0
```

See also [Example 35–3]().

10.4. Testing and Branching 121