# DESCRIPTION

**preconv** reads *files* and converts its encoding(s) to a form **GNU (1)** can process, sending the data to standard output. Currently, this ans ASCII characters and `\[uXXXX]` entities, where `XXXX` is a hexadecimal nuer with four to six digits, representing a Unicode input code. Normally, **preconv** should be invoked with the **-k** and **-K** options of **groff**.