# An Introduction to the vi Editor

![](bbox=[0.118, 0.143, 0.882, 0.283])

"buckaroo" [Read only] 8 Lines, 271 characters

Notice the addition of the [Read only] message on the status line. You can edit thenfile, if you try to save the edits with :w, you will see this:

![](bbox=[0.118, 0.403, 0.882, 0.443])

"buckaroo" File is read only

+   Quit vi with :qt.
2. Next, recall that janitor occurs in many places in the big.output file. I'll start vi
on the line that contains the pattern janitor in the file. This time, notice where
t cursor is sitting.

% vi +/janitor big.output

| brandt ttyrb | Nov 28 23:03 | (age) |
| holmes ttrj | Dec 3 21:59 | (age) |
| vyxi ttyrn | Dec 1 14:19 | (pc) |
| frodo ttyro | Dec 3 22:01 | (mentor) |
| labeck ttyrt | Dec 3 22:02 | (dow) |
| chenit2 ttyro | Dec 2 21:53 | (mentor) |
| leunto ttyso | Nov 20 15:11 | (doli) |
| chinese ttyss | Dec 3 22:53 | (excalibur) |
| cdmemert ttyss | Dec 3 23:00 | (mentor) |
| yuenca ttyss | Dec 3 23:00 | (mentor) |
| janitor ttys7 | Dec 3 18:19 | (age) |
| mathisb ttysr | Dec 3 23:17 | (dov) |
| janitor ttys9 | Dec 3 18:18 | (age) |
| cs541 ttysc | Dec 2 15:16 | (solaria) |
| yansong ttysl | Dec 1 14:44 | (cath) |
| mdbss ttyvo | Nov 30 19:39 | (localhost) |
| md ttysu | Dec 2 08:45 | (muller) |
| jac ttysa | Dec 3 18:18 | (localhost) |
| elchsted ttytb | Dec 3 22:21 | (pc) |
| sweetet ttysc | Dec 3 22:40 | (dov) |
| wellman ttysd | Dec 3 23:01 | (dov) |
| tuffleno ttyse | Dec 3 23:03 | (indexv) |
| wu ttysf | Dec 3 23:10 | (term01) |
| "big.output" 40 Lines, 1659 characters

*