

要仅追加字符串的一部分，请指定起始索引和要复制的字符数。下面的语句从 alphabet 的第五个字符开始，将最多六个字符追加到 aString：

```
aString.append(alphabet, 4, 6);
```

使用 assign() 函数可以将新的字符串，或字符串的一部分，赋给任何字符串对象。为要进行赋值的对象调用该函数。 使用本节开头那两个字符串，以下列任意一种样式调用 assign()。注释显示赋给 aString 的结果字符串：

```
aString.assign(alphabet);      // "abc...xyz"
aString.assign(alphabet, 2, 6); // "cdefgh"
aString.assign(alphabet, 20);   // "uvwxyz"
aString.assign(8, '*');         // "********"
```

第一个语句将一个字符串对象赋给另一个字符串对象，等价于以下语句：

```
aString = alphabet;
```

第二个语句从 alphabet[2] 开始向 aString 赋六个字符。第三个语句从 alphabet[20] 开始向 aString 赋字符，一直持续到源字符串的末尾。最后一个语句向 aString 赋一个由八个星号字符组成的字符串。某些版本的 ANSI C++ 也允许将字符赋给字符串，但 GNU C++ 会对以下这类语句发出错误信息：

```
aString.assign('8'); // ???
```

如果你的程序因这类语句而编译失败，请将其替换为以下语句：

```
aString.assign(1, '8');
```

## Tip

使用 string 类模板的一个缺点是，即使是简单的错误，也往往会导致 GNU C++ 显示许多行令人困惑的错误信息，其中列出了可能的“候选”函数参数。要在编译器的冗长输出中找出你的错误，请先查找行号，然后在尝试解读错误信息文本之前检查你的输入。

你也可以向 assign() 传递一对迭代器（有关迭代器的信息，请参阅第 23 章“使用标准模板库 STL”）。例如，下面的语句将字符数组的一部分赋给字符串对象：

```
char buffer[26];
strcpy(buffer, alphabet.c_str());
aString.assign(buffer + 5, buffer + 10);  // aString == "fghij"
```

你也可以传递来自任何包含字符数据的结构的迭代器对，而不仅仅是 C 风格的 char 数组。例如，下面的示例语句将字符从标准模板 vector 对象复制到字符串：

```
vector<char> v(buffer, buffer + 26);
aString.assign(v.begin(), v.end()); // aString == "abc...xyz"
```

要交换两个字符串，你可能在排序或随机化操作中这样做，使用 swap() 函数如下：

```
aString.swap(alphabet);
```

这会交换两个字符串对象 aString 和 alphabet 的值。有趣的是，哪个字符串对象执行交换并不重要——下面的语句产生的效果与前一条相同：

```
alphabet.swap(aString);
```

请注意，这里描述的函数会抛出 out_of_range 和 length_error 异常来报告错误。使用 try 和 catch 块来捕获这些错误，如下所示：

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

在调用 assign() 时使用错误的索引值（100）会导致该函数抛出 out_of_range 异常。

## INSERTING AND DELETING strings

要向字符串中插入字符并删除字符串的一部分，请调用 insert() 和 remove() 字符串类成员函数。通过调用 replace() 将这两个函数结合起来，该函数执行插入后跟删除。

Note
本节中的示例语句取自 CD-ROM 上的文件 strfn2.cpp。

按如下方式使用 insert() 在字符串的任何位置插入文本。例如，第三个语句将字符串对象 s1 设置为字符串 "It's a beautiful life"：

```
string s1 = "It's a life";
string s2 = "It's a beautiful day";
s1.insert(7, s2, 7, 10);
```

