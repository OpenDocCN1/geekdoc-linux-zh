# BUGS

**script** places *everything* in the log file, including linefeeds and backspaces. This is not what the naive user expects.

**script** is primarily designed for interactive terminal sessions, it’s possible that when stdin is not a terminal (for example “echo foo | script”) then all session hung ups, because interactive shell within script session miss EOF and the **script** has no clue when close the session. See the NOTES section for more information.