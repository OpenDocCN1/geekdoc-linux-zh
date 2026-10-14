# LISTING 13.2 CONTINUED

```
// Member function
const char *TPrompt::GetString()
{
    return tp_string;
}
```

In the original code from which I created the TPrompt class, the get_string() function returns a pointer to a dynamic string, allocated in memory by the C++ new operator. Calling the function places the responsibility of deleting that memory on the user. For example, with the original function, you might use statements such as
const char *cp = get_string("Enter a string: ");
// ... other statements
delete[] cp;

If you forget the delete[] statement, the memory allocated to the string can become lost in space, creating a memory leak that might cause the program to abort with that lovable old friend, a core dump. By encapsulating get_string() in a class, memory management is automatic, and this type of bug can't occur.

To encapsulate the original code, the TPrompt class declares one private data member, a char pointer named tp_string. Because the member is private to the class, only class members may use it. In addition, the class declares a constructor TPrompt() and destructor ~TPrompt(). The constructor code is the same as in the original get_string() function, but instead of returning a char pointer, it saves the user's input string in a memory buffer addressed by the private tp_string pointer. To use the class, the program constructs an object in the usual way with the following statement:
TPrompt prompt1("Prompt #1: ");

This creates an object, named prompt1, of the TPrompt class, and calls the class constructor to display a message and wait for the user to enter a string. Member function GetString() returns a const pointer to the input string, used here to confirm your typing:
cout << "You entered " << prompt1.GetString() << endl;

GetString() returns a const char pointer. This copies the address of the privately owned dynamic memory out of the object, but because it is declared const, the class user—that is, the preceding two statements—can't alter that memory.

> Warning
> GNU C++ reports the modification of data addressed by a const string pointer as a warning rather than an error. Apparently, this was done to accommodate existing code that uses this questionable technique.

Because the TPrompt class carefully controls the use of its private data, the class assumes all responsibility for managing the object's dynamic memory. To ensure that this memory is