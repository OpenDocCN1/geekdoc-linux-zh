With `ANSI_QUOTES` disabled, the statement selects the literal string "`last_name`" once for each row in the `president` table. With `ANSI_QUOTES` enabled, the statement selects the values of the `last_name` column from the table.

For the examples following that use the double quote as a string quoting character, assume that `ANSI_QUOTES` mode is not enabled.

MySQL recognizes several escape sequences within strings that indicate special characters, as shown in Table 3.1. Each sequence begins with a backslash character (\\) to signify a temporary escape from the usual rules for character interpretation. Note that a NUL byte is not the same as the SQL `NULL` value; NUL is a zero-valued byte, whereas `NULL` in SQL signifies the absence of a value.

| Table 3.1 | String Escape Sequences |
| :--- | :--- |
| **Sequence** | **Meaning** |
| `\\0` | NUL (zero-valued byte) |
| `\'` | Single quote |
| `\"` | Double quote |
| `\\b` | Backspace |
| `\\n` | Newline (linefeed) |
| `\\r` | Carriage return |
| `\\t` | Tab |
| `\\\\` | Single backslash |
| `\\Z` | Control-Z (Windows EOF character) |


The escape sequences shown in the table are case sensitive, and any character not listed in the table is interpreted as itself if preceded by a backslash. For example, \\t is a tab, but \\T is an ordinary "T" character.

Table 3.1 shows that you can escape single or double quotes using backslash sequences, but you actually have several options for including quote characters within string values:

+   Double the quote character if the string itself is quoted using the same character:
+   
+   *   `'I can''t.'`
+   *   `'He said, ""I told you so.""'`

+   Quote the string with the other quote character. In this case, you do not double the quote characters within the string:
+   
+   *   `"I can't."`
+   *   `'He said, "I told you so."'`