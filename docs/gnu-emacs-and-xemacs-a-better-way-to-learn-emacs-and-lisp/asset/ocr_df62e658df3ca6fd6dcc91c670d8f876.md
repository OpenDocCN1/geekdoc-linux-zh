As with the preceding function, a `let` wrapper sets up three new variables that are defined further along in the function.

Before the `while` loop begins its repetitious action, one of the new `let` variables is given a value with `setq` in line 5. This is the beginning of the counter. After each run through the `while` loop, line 12 adds 1 to the value of the variable `i`. What’s to keep this `while` loop from spinning off into an endless series of repetitions?

The condition clause in line 7 sets a boundary for the `while` loop’s repetitions. Line 7 in English could look like this:

> As long as the number of elements (or cons cells) in `clipper-alist` is greater than the current value of `i`, The `safe-length` function in line 7 is a counting function with a safety feature: If a list being counted is circular, `safe-length` restricts itself to counting only unique items.

`safe-length` returns the number of elements in `clipper-alist`. Now the function needs some way of putting together a list of clip names.

The `setq` statement in line 8 does much of the work. It sets the value of the `let` variable `clip` to a different value during each cycle of the `while` loop, depending on what the current value of `i` is. The `nth` function uses the value of `i` to retrieve the corresponding member of `clipper-alist`. This function takes two arguments: the first is a number, and the second is a list. If `i`, which is the number in the function, is 3, the function returns the third member of the list.

A problem arises, however: The members of `clipper-alist` are cons cells, composed of a clip’s name and its content. The function is trying to build a completion list from clip names; the contents of a clip are superfluous here. This is where the list operator `car` comes in handy.

The `nth` function has extracted a particular cons cell from `clipper-alist`. Taking the `car` of that cons cell results in the clip name alone. The `setq` function in line 7 takes that result and sets the value of `clip`.

In line 9, the `message` function displays the clip name in the minibuffer.

The current value of the `clip` variable, which is different each time through the `while` loop, is added to a temporary completion list by the function `add-to-list`.

When the `while` loop has finally processed each member of `clipper-alist`, the result is a completion list containing every clip name in the alist.

This serves the function in line 13, `completing-read`. This function takes two arguments. The first is a prompting string to display in the minibuffer, and the second is a completion list to search for matches. When the user types a letter in the