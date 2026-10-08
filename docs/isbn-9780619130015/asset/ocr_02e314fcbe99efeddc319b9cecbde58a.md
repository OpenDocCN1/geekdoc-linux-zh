By default, pr formats the specified files into single-column pages of 66 lines. Each page has a five-line header, which, by default, contains the current file’s name, its last modification date, current page, and a five-line trailer consisting of blank lines.

+   - **Syntax**	`pr [options] [file...]`
- **Dissection**	■ The three most frequently used options are `−h` (header-format), which lets you customize your header line; `−d`, which double-spaces output; and `−l n`, which sets the number of lines per page.

Use pr to format the unix_stuff file. Use the pipe operator (|) to send the output to more, so the output screen does not flash by.

![](bbox=[0.17, 0.37, 0.93, 0.91])