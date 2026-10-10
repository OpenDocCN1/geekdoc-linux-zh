```
```python
'goodbye'
>>> test = "Are you really Bill 0'Reilly?"
>>> test
"Are you really Bill 0'Reilly?"
```
```

The first example encapsulates the string in single quotation marks and the second and third in double quotation marks. However, printing the first and second strings shows them both in single quotation marks because Python does not distinguish between the two. The third example is the exception—it uses double quotation marks because the string itself contains a single quotation mark. Here, Python prints the string with double quotation marks because it knows the string contains the single quotation mark.

Because the characters in a string are stored in sequence, you can index into them by specifying the character in which you are interested. Like most other languages, these indexes are zero-based, which means you need to ask for character 0 to get the first letter in a string. For example:

```
```python
>>> string = 'This is a test string'
>>> string
'This is a test string'
>>> string[0]
'T'
>>> string[0], string[3], string[20]
('T', 's', 'g')
```
```

The last line shows how, with commas, you can ask for several indexes at the same time. You could print the entire first word by using this:

```
```python
>>> string[0], string[1], string[2], string[3]
('T', 'h', 'i', 's')
```
```

However, for that purpose you can use a different concept: slicing. A slice of a sequence draws a selection of indexes. For example, you can pull out the first word like this:

```
```python
>>> string[0:4]
'This'
```
```

The syntax there means “take everything from position 0 (including 0) and end at position 4 (excluding it).” So [0:4] copies the items at indexes 0, 1, 2, and 3. You can omit either side of the indexes, and it copies either from the start or to the end:

```
```python
>>> string[:4]
'This'
>>> string[5:]
'is a test string'
>>> string[11:]
'est string'
```
```