# LISTING 11.1 CONTINUED

```
size_t mem_block_size(const void *p);

int main()
{
    // Prompt user for and create a dynamic string
    const char *cp = get_string("Enter a string: ");

    // Display some statistics
    cout << "String : " << cp << endl;
    cout << "Length : " << strlen(cp) << " char(s)" << endl;
    cout << "Size   : " << mem_block_size(cp) << " bytes" << endl;

    // Delete string when finished
    delete[] cp;  // Notice the brackets!
    return 0;
}

// Prompts user to enter a string. Returns address of a new
// character buffer big enough to hold only that string.
// Be sure to delete the returned pointer!
const char *get_string(const char *prompt)
{
    const int buf_size = 128;        // Size of input buffer
    char *temp = new char[buf_size]; // Create input buffer
    cout << prompt;                  // Prompt user for input
    cin.getline(temp, buf_size);     // Read input from user
    char *result = new char[strlen(temp) + 1]; // Create string
    strcpy(result, temp);            // Copy buffer to result
    delete[] temp;                   // Delete the buffer
    return result;                   // Return entered string
}

// Return size in bytes of an allocated memory block
// addressed by pointer p. Tricky but it works.
size_t mem_block_size(const void *p)
{
    char *cp = (char *) p;   // Convert void * to
    return *(size_t *)(cp - 4); // allow math on p
    // Size of chunk is
    // four bytes back
}
```

The newstr.cpp program declares two function prototypes, get_string() and mem_block_size(). In the program, this statement prompts the user to enter a string: const char *cp = get_string("Enter a string: ");

The const char pointer cp is assigned the result of calling get_string(). The literal string parameter passed to the function is the prompt displayed onscreen. Specifying cp to be const prevents the program from attempting to modify the entered string. This isn’t strictly necessary, and you could rewrite the program to use pointers of type char *. However, because the returned string is only as long as necessary, operations that change the string’s length might be dangerous, and it is best made const for that reason.