# 32

# addbib

| Key Letter | Description |
| --- | --- |
| %J | Journal containing article. |
| %K | Keywords to use in locating reference. |
| %L | Label field used by -k option of refer. |
| %M | Bell Labs Memorandum (undefined). |
| %N | Number within volume. |
| %O | Other commentary, printed at end of reference. |
| %P | Page number(s). |
| %Q | Corporate or foreign author (unreversed). |
| %R | Report, paper, or thesis (unpublished). |
| %S | Series title. |
| %T | Title of article or book. |
| %V | Volume number. |
| %X | Abstract-used by roffbib, not by refer. |
| %Y, Z | Ignored by refer.

# Example

The following example creates a database named bibliography, displays the instructions, adds one entry, and then displays the contents of the database by means of the vi editor.

```
castle@ addbib bibliography
Instructions? y
```

Addbib will prompt you for various bibliographic fields. If you don't need a particular field, just hit Return, and that field will not appear in the output file. If you want to return to previous fields in the skeleton, a single minus sign will go back a field at a time. (This is the best way to input multiple authors.) If you have to continue a field or add an unusual field, a trailing backslash will allow a temporary escape. Finally, be prompted for an abstract in as many lines as you need, and end with a ctrl-d. To quit, type 'q' or 'n' when asked if you want to continue. To edit the database, type 'edit', 'vi', or 'ex' instead.

| Author: | Janice Winsor |
| Title: | Opening the Dream Door |
| Journal: | |
| Volume: | |
| Pages: | 153 |
| Publisher: | Merrill-West Publishing |
| City: | Carmel, California |
| Date: | 1998 |
| Other: | |