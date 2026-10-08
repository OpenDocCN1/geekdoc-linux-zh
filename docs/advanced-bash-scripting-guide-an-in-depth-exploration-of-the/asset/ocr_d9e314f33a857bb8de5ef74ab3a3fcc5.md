# Advanced Bash-Scripting Guide

```
# The replacement need not be a literal,
# since the result of a function invocation is allowed.
# This is general to all forms of replacement.
echo
echo ' - Replace first occurrence with Result-Of -'
echo ${string[123]//_simple} # Works as expected.
echo ${array[2]//ca5_simple} # Applied to each element.
echo ${sparse[2]//ca5_simple} # Works as expected.
echo
echo ' - Replace all occurrences -'
echo ${string[//b2]/X} # X-out b's and 2's
echo ${string[//abc]/xyz} # xyzABC123ABCxyz
echo ${array[//abc]/xyz} # Applied to each element.
echo ${sparse[//abc]/xyz} # Works as expected.
echo
echo ' - Delete all occurrences -'
echo ${string[//b2]//}
echo ${string[//abc]//}
echo ${array[//abc]//}
echo ${sparse[//abc]//}
echo
echo ' - Prefix sub-element replacement - -'
echo ' - Match must include the first character. -'
echo
echo ' - Replace prefix occurrences -'
echo ${string[#[b2]/X} # Unchanged (neither is a prefix)
echo ${string[#_abc]/XYZ} # XYZABC123ABCabc
echo ${array[#abc]/XYZ} # Applied to each element.
echo ${sparse[#abc]/XYZ} # Works as expected.
echo
echo ' - Delete prefix occurrences -'
echo ${string[#[b2]//}
echo ${string[#_abc]//}
echo ${array[#abc]//}
echo ${sparse[#abc]//}
echo
echo ' - Suffix sub-element replacement - -'
echo ' - Match must include the last character. -'
echo
echo ' - Replace suffix occurrences -'
echo ${string[#[b2]/X} # Unchanged (neither is a suffix).
echo ${string[#_abc]/XYZ} # abcABC123ABCXYZ
echo ${array[#abc]/XYZ} # Applied to each element.
echo ${sparse[#abc]/XYZ} # Works as expected.
echo
echo ' - Delete suffix occurrences -'
echo ${string[#[b2]//}
echo ${string[#_abc]//}
echo ${array[#abc]//}
echo ${sparse[#abc]//}
echo
echo ' - Special cases of null Glob-Pattern - '
```

Appendix A. Contributed Scripts

782