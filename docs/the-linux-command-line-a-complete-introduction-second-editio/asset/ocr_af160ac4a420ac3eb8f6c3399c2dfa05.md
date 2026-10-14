![](bbox=[0.129, 0.091, 0.864, 0.426])

*Figure 22-1: Viewing a2ps output*

As we can see, the default output layout is “two-up” format. This causes the contents of two pages to be printed on each sheet of paper. a2ps applies nice page headers and footers, too.

a2ps has a lot of options. Table 22-4 provides a summary.

**Table 22-4: a2ps Options**

| Option | Description |
|---|---|
| `--center-title=text` | Set center page title to *text*. |
| `--columns=number` | Arrange pages into *number* columns. The default is 2. |
| `--footer=text` | Set page footer to *text*. |
| `--guess` | Report the types of files given as arguments. Since a2ps tries to convert and format all types of data, this option can be useful for predicting what a2ps will do when given a particular file. |