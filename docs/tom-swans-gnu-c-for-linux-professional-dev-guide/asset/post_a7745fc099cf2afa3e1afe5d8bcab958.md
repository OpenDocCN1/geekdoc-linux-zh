
To append only a portion of a string, specify a starting index and the number of characters to copy. The following statement appends up to six characters from alphabet to aString starting with the fifth character:

```
aString.append(alphabet, 4, 6);
```

Use the assign() function to assign a new string, or portions of a string, to any string object. Call the function for the object to which you want to make the assignment. Using the two strings from the beginning of this section, call assign() using any of the following styles. Comments show the resulting strings assigned to aString:

```
aString.assign(alphabet);      // "abc...xyz"
aString.assign(alphabet, 2, 6); // "cdefgh"
aString.assign(alphabet, 20);   // "uvwxyz"
aString.assign(8, '*');         // "********"
```

The first statement assigns one string object to another and is equivalent to the following:

```
aString = alphabet;
```

The second statement assigns six characters to aString starting from alphabet[2]. The third statement assigns characters to aString starting from alphabet[20] and continuing to the end of the source string. The last statement assigns a string of eight asterisk characters to aString. Some versions of ANSI C++ also permit assigning characters to strings, but GNU C++ issues an error message for statements such as this:

```
aString.assign('8'); // ???
```

If your program fails to compile because of this kind of statement, replace it with the following:

```
aString.assign(1, '8');
```

## Tip

One disadvantage of using the string class template is that even a simple mistake tends to cause GNU C++ to display many lines of confusing error messages listing possible "candidate" function arguments. To find your mistake in the midst of the compiler's wordy output, hunt for the line number first and then check your typing before attempting to decipher the error message's text.

You can also pass a pair of iterators to assign() (see Chapter 23, "Using the Standard Template Library (STL)" for information about iterators). For example, the following statements assign a portion of a character array to a string object:

```
char buffer[26];
strcpy(buffer, alphabet.c_str());
aString.assign(buffer + 5, buffer + 10);  // aString == "fghij"
```

You may also pass a pair of iterators from any structure that contains character data, not only a C-style array of char. The following sample statements, for example, copy characters from a standard template vector object to a string:

```
vector<char> v(buffer, buffer + 26);
aString.assign(v.begin(), v.end()); // aString == "abc...xyz"
```

To swap two strings, which you might do in a sorting or randomizing operation, use the swap() function like this:

```
aString.swap(alphabet);
```

That swaps the values of the two string objects aString and alphabet. Interestingly, it doesn't matter which string object does the swapping—the following statement produces the same results as the preceding:

```
alphabet.swap(aString);
```

Be aware that the functions described here throw out_of_range and length_error exceptions to report errors. Use try and catch blocks to trap these errors as follows:

```
try {
  cout << "Intentional error follows..." << endl;
  aString.assign(alphabet, 100); // Force exception
  show("After assign with bad index");
}
catch (out_of_range err) {
  cout << "*** Range error: " << err.what() << endl;
}
catch (length_error err) {
  cout << "*** Length error: " << err.what() << endl;
}
```

The use of a bad index value (100) in calling assign() causes that function to throw an out_of_range exception.

## INSERTING AND DELETING strings

To insert characters into strings, and to delete portions of strings, call the insert() and remove() string-class member functions. Combine the two functions by calling replace(), which performs an insertion followed by a removal.

Note
The sample statements in this section are taken from file strfn2.cpp on the CD-ROM.

Use insert() as follows to insert text anywhere in a string. For example, the third statement sets string object s1 to the string "It's a beautiful life":

```
string s1 = "It's a life";
string s2 = "It's a beautiful day";
s1.insert(7, s2, 7, 10);
```
