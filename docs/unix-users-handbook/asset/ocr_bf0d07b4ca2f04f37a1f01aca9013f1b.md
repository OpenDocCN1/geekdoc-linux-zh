# ## Copying Text in vi

You can copy text in vi. Some commands for copying are shown in Table 8-7.

# **Table 8-7 Copying In vi**

| Command | Copy Action |
| :--- | :--- |
| yy | Yank the current line. |
| nyy | Yank **n** lines. |
| p (lower case) | Put the yanked text after the cursor. |
| P (upper case) | Put the yanked text before the cursor. |
| "(a-z)nyy | Copy *n* lines into the buffer named in parentheses. Omit *n* for the current line. |
| "(a-z)ndd | Delete *n* lines into the buffer named in parentheses. Omit *n* for the current line. |
| "(a-z)p | Put lines named in the buffer in parentheses after current line. |
| "(a-z)P | Put lines named in the buffer in parentheses before the current line. |


Let’s now look at some examples of copying text in **wisdom** in Figure 8-13.