+   - If the search has not found what you want but to stay at the current position, press RETURN to stop the search at that point.
- If the search has gone wrong and you just want to get back to where you started, press CONTROL-6 (the quit character). From an unsuccessful search single CONTROL-6 backs out all the characters in the search string that could not be found. If this takes you back to a place you wish to continue searching from, you can add characters to the search string again. If you do not want to continue the search from here, a second CONTROL-6 ends the search and leaves the cursor where it was to begin with.

# Nonincremental Searches

If you prefer that your searches succeed or fail without showing all the intermediate results, you can give the nonincremental commands CONTROL-S RETURN to search forward or CONTROL-R RETURN to search backward. Searching does not begin until you enter a search string in response to the emacs prompt and press RETURN again. Neither of these commands wraps the past end of the buffer.

# Regular Expression Searches

You can perform both incremental and nonincremental regular expression searching in emacs. To begin a regular expression search, you can use the commands listed in Table 11-2.

| Searching for Regular Expressions | table 11-2 |
|---|---|
| META-CONTROL-X | Incrementally searches forward for regular expression; prompts for a regular expression one character at a time |
| META-xisearch-backward-regexp | Incrementally searches backward for regular expression; prompts for a regular expression one character at a time |
| META-CONTROL-S RETURN | Prompts for and then searches forward for a complete regular expression |
| META-x isearch-backward-regexp RETURN | Prompts for and then searches backward for a complete regular expression |