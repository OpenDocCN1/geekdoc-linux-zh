# Wildcards and Regular Expressions

# Task 9.5: For Complex Expressions, Try egrep

Sometimes a single regular expression can't locate what you seek. Perhaps you're looking for lines that have either one pattern or a search pattern. That's where the egrep command proves helpful. The command gets its name from "expression grep," and it has a notational scheme more powerful than that of grep, as shown in Table 9.3.

Table 9.3. Regular expression notation for egrep.
| Notation | Meaning |
|---|--|
 c | Matches the character c |
| \c | Forces c to be read as the letter c, not as another meaning the character might have |
| ^ | Beginning of the line |
| $ | End of the line |
| . | Any character |
| [xy] | Any single character in the set specified |
| [^xy] | Any single character not in the set specified |
| c* | Zero or more occurrences of character c |
| c+ | One or more occurrences of character c |
| c? | Zero or one occurrences of character c |
| a|b | Either a or b |
| (a) | Regular expression |

+   1. Now I'll search the password file with grep to demonstrate egrep. A pattern that seemed a bit weird we used with grep to search for lines containing one or more occurrences of the letter z: "zz". With egrep, this search is much easier:
```bash
% grep "za*" /etc/passwd | head
marg?:724:1233:Guzyee/users/marg/bin/ksh\axy?:1272:1233:martine/users/bin/csh
wizard?:1650:1975:022:users/vizard/bin/ksh
zhg?:7227:1318:Zhong/users/bin/csh
mm?:7152:1233:michael Kennedy/users/bin/csh
tanzm?:7368:1140:Zen Tan/users/tanzm/bin/csh
mendoz?:8467:1293:Don Mendoza/users/mendoz/bin/csh
pazvy?:9485:1769:Lucky/users/pazvy/bin/csh
hurliz?:9189:1375:Tom Hurley/users/hurliz/bin/csh
tulip?:9222:1375:Liz Richards/users/tulip/bin/csh
Broken pipe
```