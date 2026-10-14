
After making whatever changes you want to the string, assign the modified buffer to the object using a statement such as this:

```cpp
sobject4.assign(buffer);
```

## COMPARING AND SEARCHING string Objects

Two of the most common operations performed on string data are comparing and searching. With C-style strings, these jobs usually require revisiting the online documentation for functions such as `strcmp()` and `strstr()`—at least that’s true for me because I can never remember which arguments to use in what order. With string class objects, as the following sections explain, comparing and searching is intuitive and less likely to lead to hard-to-find bugs.

### Comparing string Objects

Compare string objects using the same logical operators that you use in mathematical expressions. For example, if `s1` and `s2` are string class objects, you can compare them in statements such as these:

```cpp
if (s1 == s2) ...  // Do if s1 equals s2
if (s1 <  s2) ...  // Do if s1 is less than s2
if (s1 >  s2) ...  // Do if s1 is greater than or equal to s2
if (s1 != s2) ...  // Do if s1 is not equal to s2
```

Those and similar expressions are possible because the string class overloads C++ logical operators. The string class doesn’t overload all C++ operators; only those that are sensibly used with string objects. You can’t, for example, apply the increment operator to string objects. These statements do not compile:

```cpp
s1++;  // ???
s2++;  // ???
```

If you prefer to call a function to compare string objects, use the string class’s `compare()` member function. This function is useful also for comparing portions of strings. To try `compare()`, define some variables such as these:

```cpp
int result, pos, count;
string s1, s2;
```

> **Note**
> 
> The programming in this section is taken from file compare.cpp on the CD-ROM in the src/c22 directory.

There are three basic forms of `compare()`, all of which return an integer result:

```cpp
result = s1.compare(s2, pos, count);
result = s1.compare("Literal string", pos);
result = s1.compare("Literal string", pos, count);
```

statements display a value greater than the length of alphabet, indicating that there are no White Elephants in the alphabet.

Instead of literal strings, you can pass string objects to find() and rfind() to perform searches. These statements display 12, the index of the search string object in the alphabet:

```cpp
string search = "mnop";
cout << alphabet.find(search) << endl;
```

As you can with compare(), you can also specify a starting position to begin the search somewhere other than its beginning or end:

```cpp
cout << alphabet.find(search, 4) << endl;
```

That also displays 12, but change 4 to 15 and find()’s return value indicates that it can’t find the substring. To search backward from a starting position, specify an index value to rfind(). The following does not find xyz in the alphabet because it searches from index 10 to the beginning:

```cpp
cout << alphabet.rfind("xyz", 10) << endl;
```

The find() and rfind() functions can also search for characters in a string object:

```cpp
cout << alphabet.find('z') << endl;
cout << alphabet.rfind('a') << endl;
```

Other string-search functions locate the first character from a character set, represented by a string object. Given the alphabet string defined at the beginning of this section, the following statements show how to use these functions, find_first_of() and find_last_of():

```cpp
string vowels("aeiou");
cout << alphabet.find_first_of(vowels) << endl;  // 0
cout << alphabet.find_last_of(vowels) << endl;   // 20
```

Use find_first_of() to locate the index of the first occurrence of any characters in the argument string (vowels in this example). Use find_last_of() to locate the last such index. The preceding statements report 0 and 20 as shown in the comments.

Use these functions’ "not" counterparts, find_first_not_of() and find_last_not_of(), to locate the first nonmatching characters of a set. The following statements find the first and last nonvowel indexes in the alphabet string (the function results are shown as comments):

```cpp
cout << alphabet.find_first_not_of( vowels ) << endl;  // 1
cout << alphabet.find_last_not_of( vowels ) << endl;   // 25
```

Specify a starting index to search for character sets in a string at a position other than the beginning or end. This is useful for continuing a search for characters as demonstrated by the following while loop that finds all vowels in the alphabet:

```cpp
int p = alphabet.find_first_of( vowels );
while ( p < alphabet.length() ) {
    cout << "'" << setw(2) << p << "] == ";
    cout << alphabet[p] << "'" << endl;
    p = alphabet.find_first_of( vowels, p + 1 );
}
```
