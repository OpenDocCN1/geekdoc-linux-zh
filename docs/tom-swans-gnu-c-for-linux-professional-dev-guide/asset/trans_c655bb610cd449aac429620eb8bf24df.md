

## LISTING 11.1 CONTINUED

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

newstr.cpp 程序声明了两个函数原型，get_string() 和 mem_block_size()。在程序中，这条语句提示用户输入一个字符串：const char *cp = get_string("Enter a string: ");

const char 指针 cp 被赋值为调用 get_string() 的结果。传递给函数的字面量字符串参数是屏幕上显示的提示。指定 cp 为 const 可以防止程序尝试修改输入的字符串。这并不是严格必要的，你也可以重写程序使用类型为 char * 的指针。然而，由于返回的字符串仅与所需长度一样长，改变字符串长度的操作可能会很危险，因此最好将其设为 const。

使用完字符串后，使用 delete 运算符的特殊形式将其删除：

```
delete[] cp;
```

空括号通知编译器 cp 指向一个数组。在这种情况下，括号并不是严格需要的，因为数组只包含简单的 char。然而，正如你在下一节中所学到的，其他类型的数组在删除时可能需要特殊处理，因此养成使用 delete[] 来删除动态数组是一个好习惯。

现在来看 get_string() 函数。它首先声明一个常量整数 buf_size，等价于 128。这是函数可以返回的最大大小。你可能想将其值改为 255 或更高，特别是在使用此方法从文件读取字符串时。接下来，函数创建一个声明的最大大小的动态缓冲区：

```
char *temp = new char[buf_size];
```

几条 I/O 语句提示用户将字符串输入到临时缓冲区中，由 cin.getline() 函数读取。标准 C 库字符串函数 strlen() 和 strcpy() 用于创建一个刚好足够容纳输入字符串的对象，并将输入字符串复制到该位置：

```
char *result = new char[strlen(temp) + 1];
strcpy(result, temp);
```

第一条语句调用 strlen() 来获取存储在临时缓冲区中的输入字符串的长度。因为该长度不包括字符串末尾的空终止符，所以语句在传递给 new 的值上加 1。char * 变量 result 现在指向一个恰好足够容纳输入字符串的字符串缓冲区，由 strcpy() 转移到保留的空间中。最后，get_string() 调用 delete[] 删除临时缓冲区，并返回指向缩小尺寸动态字符串的指针。

> 如果频繁调用 get_string()，创建一个固定的全局输入缓冲区供函数使用，而不是每次调用函数时都创建一个临时缓冲区，可能会更有优势。

运行程序时，它会提示你输入一个字符串。在你按下 Enter 后，程序会显示你的输入和字符串的长度。它还会显示 new 分配的内存块的大小。以下是一个示例运行：

```
$ ./a.out
Enter a string: Testing, one, two, three
String : Testing, one, two, three
Length : 24 char(s)
Size   : 32 bytes
```

字符串的长度只是通过调用 strlen() 确定的。然而，内存块的大小可能会让你感到惊讶。在这种情况下，24 字节的字符串实际上在内存中占用了 32 字节的空间。在试图节省内存的尝试中，程序显然浪费了 8 字节。这肯定比使用固定长度的 128 字节

