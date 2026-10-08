# 1232 sccs-prs, prs

-cdate-time Display information on the latest delta checked before the date and time indicated by the date-time argument. date-time takes the form yy[:mm[dd[hh[:mm[:ss]]]]]].

+   -dataspec Produce a report according to the indicated data specification. Specify dataspec as a quoted string that includes embedded data keywords of the form 'key:'. The prs command expands keywords in the output it produces. To specify a Tab character in the output, use \t; to specify a newline in the output, use \n.

+   -rsid Specify the SCCS delta ID (sid) of the delta for which you want information. If you specify no sid, use the most recently created delta.

# Usage

# Data Keywords

Data keywords specify which parts of an SCCS file are to be retrieved. All parts of an SCCS file (see sfile(4)) have an associated data keyword. A data keyword can appear any number of times in a data specification argument to -d. These keywords are listed in the following table.

In the Section column, B = body, D = delta table, F = flags, and U = user names. In the Format column, S = simple format and M = multiline format.

| Keyword | Data Item | Section | Value | Format |
| --- | --- | --- | --- | --- |
| :A: | Format for the string | N/A | :Z::Y: :M | S |
| :B: | Branch number | D | nnnn | S |
| :BD: | Body | B | text | M |
| :BF: | Branch flag | F | yes or no | S |
| :CB: | Ceiling boundary | F | :R: | S |
| :C: | Comments for delta | D | :text | M |
| :D: | Date delta created | D | :Dy: /Dm: /Dd: | S |
| :Dd: | Day delta created | D | nn | S |
| :Dg: | Deltas ignored (seq #) | D | :DS: DS... | S |
| :DI: | Seq # of deltas included | D | :Dn: /Dx:/Gy: | S excluded ignored |
| :DL: | Delta line statistics | D | :Li:/Ld:/Lu: | S |