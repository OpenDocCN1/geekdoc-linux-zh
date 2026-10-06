| Left | File | Command | Options | Right | [|> |
|---|---|---|---|---|---||
| ~/playground/diri | .[]] | ~/playground | [|> |
| 'n Name | Size | Modify time | 'n Name | Size | 18:06 |
| .. file | Copy | 18:12 |
| Copy file "file" with source mask: | 18:07 |
| to: | [X] using shell patterns | 18:08 |
| home/me/playground/dir1/ | Dive into subdir if exists | 18:08 |
| [ ] follows | [ ] Stable Symlinks | |
| [X] Preserve attributes | | |
| < * O> [ Background ] [ Cancel | |

| UP-DIR 2996/S872M (S1%) 2996/S872M (S1%) |

Hint: Tired of these messages? Turn them off from the Options/Layout menu.
1 Help 2 Mem 3 Edit 4 Copy 5 GenMem 7 Mdir 8 Delete 9 View 10 Quit

# Renaming a file during copy

Again, this is pretty straightforward. But let's say we tagged a group of files and wanted to copy and rename them as they are copied (or move). How would we do that? Midnight Commander provides a way of doing it, but it's a little strange.

The secret is using source mask in the copy. At first, it appears that the source mask is a selection wildcard, but first appearances can be deceiving. The mask filters files as we expect, but only in a limited way. Unlike the range of wildcards available in the shell, the wildcards in the source mask are limited to "?" (for matching single characters) and "*" (for matching multiple characters). What's more, wildcards have a special property.

It works like this: let's say we want to copy (or move) it to dir with an embedded space such as "ugly file" and want to use "* instead. Using the source mask, we could enter the mask "* which means the source file name into two blocks of text separated by a space. This wildcard pattern will match the ugly file, since its name consists of two strings of characters separated by a space. Midnight Commander will associate each block of text with a number starting at 1, so block 1 will contain "ugly" and block 2 contain "file". Each block can be referred to by a number with regular expression grouping. To create a new file name for our target without the embedded space, we would specify "1\2" in the "to" field of the copy dialog like so:

14 Midnight Commander