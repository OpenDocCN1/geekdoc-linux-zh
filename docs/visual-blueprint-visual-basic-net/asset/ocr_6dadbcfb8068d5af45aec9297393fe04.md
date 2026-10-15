# WORK WITH STRINGS

Visual Basic .NET contains a number of methods that you can use to manipulate string data. You use these commands to perform actions such as cutting the string into pieces, retrieving the length of the string, and searching for sub-strings.

The Length method of a String class lets you determine the length of a string. Length takes no parameters and returns an Integer representing the number of characters in the string, including spaces and any other special characters.

PadLeft takes the content of its string and uses spaces to right-align the string to the length you specify as the parameter to the method. For example, if x = "dog" and you call x.PadLeft(5), the method returns two spaces in front of the word. PadRight has the same function, adding spaces to the right of the word.

You can use the Insert method to insert a string at a particular location. The format of the method is Insert(startPosition, stringToInsert). For example, if a = "John is a boy" and b = "bad", then a.Insert(10, b) returns "John is a bad boy".

You can use Remove to remove a known length of characters from the string. The format of the method is Remove(startPosition, length). In the preceding example, assuming the Insert command saves to string c, c.Remove(10, 4) removes the substring.

ToUpper and ToLower convert the string to uppercase and lowercase strings, respectively. They take no parameters.

The methods available in the String class do not alter the string the class represents; instead, each method returns a new string. For example, to save the lowercase string returned by ToLower back into the string where you call the method, you can use this line: a = a.ToLower().

![](bbox=[0.05, 0.6, 0.95, 0.86])

+   1 Create a new project or open an existing one.

+   2 Open the code module where you want the string manipulation to occur.

+   3 Declare a string and set its contents.

+   4 Declare a string to use for storage of the manipulated string.

Note: For more information on strings, see the section "Create a String".