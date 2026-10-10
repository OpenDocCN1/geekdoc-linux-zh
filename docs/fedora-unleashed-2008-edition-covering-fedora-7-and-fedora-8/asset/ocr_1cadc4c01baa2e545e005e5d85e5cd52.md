| Element | Explanation |
| $string=- | Performs this pattern match on the text found in the variable called `$string.` |
| s | Substitutes one text string for another. |
| / | Begins the text to be matched. |
| bob;mary | Matches the text `bob` or `mary`. You should remember that it is looking for the text `mary,` not the word `mary;` that is, it will also match the text `mary` in the word `maryland.` |
| / | Ends text to be matched; begins text to replace it. |
| fred | Replaces anything that was matched with the text `fred.` |
| / | Ends replace text. |
| g | Does this substitution globally; that is, replaces the match text wherever in the string you match it (and any number of times). |
| i | Make the search text case insensitive. It matches `bob, Bob,` or `bOB.` |
| ; | Indicates the end of the line of code. |

If you are interested in the details, you can get more information from the regex (?) section of the manual.

Although replacing one string with another might seem a rather trivial task, the code required to do the same thing in another language (for example, C) is rather daunting unless supported by additional subroutines from external libraries.

# # Access to the Shell

Perl can perform any process you might ordinarily perform if you type commands to the shell through the `` ` `` syntax. For example, the code in Listing 25.4 prints a directory listing.

```
```
$curr_dir = `pwd`;
@listing = `ls -al`;
print "Listing for $curr_dir\n";
foreach $file (@listing) {
print "$file";
}
```
```

> **NOTE**
> The `` ` `` notation uses the backtick found above the Tab key (on most keyboards), not the single quotation mark.