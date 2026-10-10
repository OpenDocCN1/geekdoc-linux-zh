OPTIONS

| Use This Option | To Do This |
| :--- | :--- |
| ** --block-r*=num, -1 num *n | Set the maximum output block length to *n* (PFB files only). |
| ** --line-length*=n, -1 *n | Set the maximum length of encrypted lines in the output to *n* (PFA files only). |
| ** --pfa, -a | Output in PFA (ASCII) format. |
| ** --pfb, -b | Output in PFB (binary) format. This is the default. |

# t1binary

**t1binary [ option | [ *input.pfa* [ *output.pfb* ] ]**

Converts the Type 1 PFA (ASCII) font specified by *input.pfa* to a font file (*output.pfb*) in PFB (binary) format. This utility is part of the Type 1 Utilities package, which is available at http://www.1cdf.org/~eddtwo/type/. *See also tlascii*.

OPTIONS

| Use This Option | To Do This |
| :--- | :--- |
| ** --block-length*=n, -1 *n | Set the maximum length of sections in PFB output to *n*. The default is to output sections as large as possible. |

EXAMPLE

| This Command | Does the Following |
| :--- | :--- |
| t1binary myfont.pfa myfont.pfb | Converts *myfont.pfa* (ASCII format) to *myfont.pfb* (binary format). |