# Advanced Bash-Scripting Guide

```
echo
echo ' - Prefix all -'
# null substring pattern means 'prefix'
echo $ {stringZ}/#NEW      # NewabcABC123Ababc
echo $ {array[@]}/#NEW   # Applied to each element.
echo $ {sparseZ[@]}/#NEW # Applied to null-content also.
                                     # That seems reasonable.
```

```
echo
echo ' - Suffix all -'
# null substring pattern means 'suffix'
echo $ {stringZ}/#NEW      # abcABC123abcNEW
echo $ {array[@]}/#NEW   # Applied to each element.
echo $ {sparseZ[@]}/#NEW # Applied to null-content also.
                                     # That seems reasonable.
```

```
echo
echo ' - Special case For-Each Glob-Pattern - '
echo ' - This is a nice-to-have dream -'
}
_GenFunc() {
    echo -n $0                  # Illustration only.
    # Actually, that would be an arbitrary computation.
}
```

```
# All occurrences, matching the AnyThing.
# //* does not match null-content nor null-reference.
# #/ / does not match null-content nor not-reference.
echo $ {sparseZ[@]}//*/ _GenFunc($)
```

```
# A possible syntax to be make
# +- the parameter used within this construct mean:
# $(1) The full element
# $(2) The prefix, if any, to the matched sub-element
# $(3) The matched sub-element
# $(4) The suffix, if any, to the matched sub-element
```

```
echo $ {sparseZ[@]}//*/ _GenFunc($)} # Same as $(1) here.
# Perhaps it will be implemented in a future version of Bash.
```

Example A-59. Testing execution times of various commands

```
#!/bin/bash
# test-execution-time.sh
# Example by Erik Brandsberg, for testing execution time
# of certain operations.
# Referenced in the "Optimizations" section of "Miscellany"

count=50000
echo "Math tests"
echo "Math via \$(())"
time for ((i=0; i<$count; i++))
do
    result=$($1 $2))
done
```

Appendix A. Contributed Examples