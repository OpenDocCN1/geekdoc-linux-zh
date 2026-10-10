# ## Holding Space

The *pattern space* is an active buffer area that holds the text examined by the *sed* editor while it processes commands. However, it isn't the only space available in the *sed* editor for storing text. The *sed* editor utilizes another buffer area called the *hold space*. You can use the hold space to temporarily hold lines of text while working on other lines in the pattern space. The five commands associated with operating with the hold space are shown in Table 21.1.

TABLE 21.1 The sed Editor Hold Space Commands

| Command | Description |
|---|---|
| h | Copies pattern space to hold space |
| H | Appends pattern space to hold space |
| g | Copies hold space to pattern space |
| G | Appends hold space to pattern space |
| x | Exchanges contents of pattern and hold spaces |

These commands let you copy text from the pattern space to the hold space. This frees up the pattern space to load another string for processing.

Usually, after using the h or H command to move a string to the hold space, eventually you want to use the g, G, or x command to move the stored string back into the pattern space (otherwise, you wouldn't have cared about saving it in the first place).

With two buffer areas, trying to determine what line of text is in which buffer area can sometimes get confusing. Here's a short example that demonstrates how to use the h and g commands to move data back and forth between the *sed* editor buffer spaces:

```
```
$ cat data2.txt
Header Line
First Data Line
Second Data Line
End of Data Lines
$
$ sed -n '/First/ {
> h ; p ;
> n ; p ;
> g ; p ;
> ' data2.txt
First Data Line
Second Data Line
First Data Line
$```
```