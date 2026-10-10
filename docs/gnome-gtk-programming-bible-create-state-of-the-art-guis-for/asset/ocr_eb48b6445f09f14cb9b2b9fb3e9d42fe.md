# # Create Cursor from XPM

A cursor also can be created from XPM data, but you must leave out the color information. The following example does this by choosing one of the XPM letters to represent the “black” color and another to represent the “white” color. Cursors usually are painted as black and white, but as this example shows, you can pick any two colors you like. All pixels that are neither black nor white are transparent.

The contents of the file sancha.xpm look like this:

```
```text
/* XPM */
/* sancha.xpm **/
static char *sancha[] = {
"24 24 5 1",
" c none",
"B c Black",
"W c White",
"r c Red",
"y c Yellow",
"rWrrWWWWWW WWWWWWWWrn",
"rrWBBB BB rWWWBBBBBWrn",
"rrrWBBBBBB WWWBBBWrn",
"rrrWWWBBBBWWW WWWBBBWrn",
"rrrWBBBBBB WWWBBBWrn",
"rrrrWWWWWWWW WWWWWWWWWW",
"rrrWWWWW WWWWWWWWrn",
"rrrWBBBBBBBBBBBBBBWrn",
"rrrrWBBB BBBB BBBBWWrrr",
"rrrrrrWBBBBB BBBB WWrrrr",
"rrrrrrrrWWBBBBBBBBWWrrrrrr",
"rrrrrrrrrrWWBBBBWWrrrrrrrr",
"rrrrrrrrrrrrWWBBWWrrrrrrrrrr",
"rrrrrrrrrrrrrWWBBWWrrrrrrrrrrrr",
"rrrrrrrrrrrrrrWWBBWWrrrrrrrrrrrrrr",
"yyyyyyyyyyyyyyyyyyyyyyyyyyyyy",
"yyyyyyyyyyyyyyyyyyyyyyyyyyyyy",
"yyyyyyyyyyyyWWBBWWyyyyyyyyyyyyyyyy",
"yyyyyyyyyyyyWBBBBBWWyyyyyyyyyyyyyyyy",
"yyyyyyyyyyyyWWBBWWyyyyyyyyyyyyyyyy",
"yyyyyyyyyyyyyyyyyyyyyyyyyyyyy",
"yyyyyyyyyyyyyyyyyyyyyyyyyyyyy",
"yyyyyyyyyyyyyyyyyyyyyyyyyyyyy",
"WWWWWWWWWWWWWWWWWWWWWWWWWW",
"WB WBBBBBBBBBBBBBBBBBBBBBWWW",
"WWWWWWWWWWWWWWWWWWWWWWWWWW"
};
```
```

This XPM definition contains five colors. It is made up of a central black area outlined in white; the background on each side is red and yellow. There is a transparent area at the top. It is shown in Figure 7-8.