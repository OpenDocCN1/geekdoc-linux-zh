# ## Tapes and Floppy Diskettes

| COMMAND | DESCRIPTION |
| :--- | :--- |
| `fdformat` | Format a floppy diskette |
| `backup` | Back up individual files<br>Use `-i` option to read file names from standard input<br>Use `-v` (verbose) option to list files as they are backed up<br>Example:<br>`$ backup -iv -t/dev/rmt0 filename1