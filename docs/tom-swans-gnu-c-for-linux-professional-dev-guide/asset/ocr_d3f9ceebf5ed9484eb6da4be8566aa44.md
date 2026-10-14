statements display a value greater than the length of alphabet, indicating that there are no White Elephants in the alphabet.

Instead of literal strings, you can pass string objects to find() and rfind() to perform searches. These statements display 12, the index of the search string object in the alphabet:

```
string search = "mnop";
cout << alphabet.find(search) << endl;
```

As you can with compare(), you can also specify a starting position to begin the search somewhere other than its beginning or end:

```
cout << alphabet.find(search, 4) << endl;
```

That also displays 12, but change 4 to 15 and find()’s return value indicates that it can’t find the substring. To search backward from a starting position, specify an index value to rfind(). The following does not find xyz in the alphabet because it searches from index 10 to the beginning:

```
cout << alphabet.rfind("xyz", 10) << endl;
```

The find() and rfind() functions can also search for characters in a string object:

```
cout << alphabet.find('z') << endl;
cout << alphabet.rfind('a') << endl;
```

Other string-search functions locate the first character from a character set, represented by a string object. Given the alphabet string defined at the beginning of this section, the following statements show how to use these functions, find_first_of() and find_last_of():

```
string vowels("aeiou");
cout << alphabet.find_first_of(vowels) << endl;  // 0
cout << alphabet.find_last_of(vowels) << endl;   // 20
```

Use find_first_of() to locate the index of the first occurrence of any characters in the argument string (vowels in this example). Use find_last_of() to locate the last such index. The preceding statements report 0 and 20 as shown in the comments.

Use these functions’ "not" counterparts, find_first_not_of() and find_last_not_of(), to locate the first nonmatching characters of a set. The following statements find the first and last nonvowel indexes in the alphabet string (the function results are shown as comments):

```
cout << alphabet.find_first_not_of( vowels ) << endl;  // 1
cout << alphabet.find_last_not_of( vowels ) << endl;   // 25
```

Specify a starting index for search for character sets in a string at a position other than the beginning or end. This is useful for continuing a search for characters as demonstrated by the following while loop that finds all vowels in the alphabet:

```
int p = alphabet.find_first_of( vowels );
while ( p < alphabet.length() ) {
    cout << "'a' set(2) << p << ']' == ";
    cout << alphabet[p] << '\' << endl;
    p = alphabet.find_first_of( vowels, p + 1 );
}
```