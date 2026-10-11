
## 字符串

字符串是表示和存储字符序列的对象。例如，你可以在代码中拥有一个通用的问候语 ‘Welcome’，并将其作为一个字符串分配给程序中的任意位置调用。

### 字符串理论

创建字符字符串有不同的方法，这些方法在历史上都是从原始 C 语言继承而来，并且至今仍被 C++ 支持。

- **步骤 1**
  
  要创建一个字符串，你需要使用 char 函数。打开一个新的 C++ 文件，并以常规的头文件开始：
  
  ```cpp
  #include <iostream>
  using namespace std;
  
  int main ()
  {
  }
  ```
  
  strings.cpp
  
  ```
  1. #include <iostream>
  2. using namespace std;
  3.
  4. int main()
  5. {
  6. 
  7. 
  8. }
  ```

- **步骤 2**
  
  很容易将字符串与数组混淆。这里是一个数组，它可以用空字符结尾：
  
  ```cpp
  #include <iostream>
  using namespace std;
  
  int main ()
  {
      char greet[8] = {'W', 'e', 'l', 'c', 'o', 'm', 'e', '\0'};
      cout << greet << "\n";
  }
  ```
  
  strings.cpp
  
  ```
  1. #include <iostream>
  2. using namespace std;
  3.
  4. int main()
  5. {
  6.    char greet[8] = {'W', 'e', 'l', 'c', 'o', 'm', 'e', '\0'};
  7.    cout << greet << "\n";
  8. }
  ```

- **步骤 3**
  
  构建并运行代码，屏幕上会出现 ‘Welcome’。虽然这完全没问题，但它不是一个字符串。字符串是一个类，它定义的对象可以表示为字符流，并且不需要像数组那样以特定方式结尾。因此，代码可以表示为：
  
  ```cpp
  #include <iostream>
  using namespace std;
  
  int main ()
  {
      char greet[] = "Welcome";
      cout << greet << "\n";
  }
  ```
  
  strings.cpp
  
  ```
  1. #include <iostream>
  2. using namespace std;
  3.
  4. int main()
  5. {
  6.    char greet[] = "Welcome";
  7.    cout << greet << "\n";
  8. 
  9. 
  10. }
  ```

- **步骤 4**
  
  在 C++ 中，还有一个 string 函数，其工作方式非常相似。再次使用问候代码，你可以输入：
  
  ```cpp
  #include <iostream>
  using namespace std;
  
  int main ()
  {
      string greet = "Welcome";
      cout << greet << "\n";
  }
  ```
  
  strings.cpp
  
  ```
  1. #include <iostream>
  2. using namespace std;
  3.
  4. int main()
  5. {
  6.    string greet = "Welcome";
  7.    cout << greet << "\n";
  8. 
  9. 
  10. }
  ```

- **步骤 5**
  
  你还可以对 string 函数应用许多不同的操作。例如，要获取字符串的长度，你可以使用：
  
  ```cpp
  #include <iostream>
  using namespace std;
  
  int main ()
  {
      string greet = "Welcome";
      cout << "The length of the string is: ";
      cout << greet.size() << "\n";
  }
  ```
  
  ![](img/4aefeb2d095f688b34af6207870c5f39_56_0.png)

- **步骤 6**
  
  可以看到，我们使用 `greet.size()` 输出了字符串内容的长度，即字符数。显然，如果你将字符串命名为 `greet` 以外的其他名称，则需要更改命令以反映这一点。它始终是“字符串名称.操作”。构建并运行代码以查看结果。
  
  ![](img/4aefeb2d095f688b34af6207870c5f39_56_1.png)

- **步骤 7**
  
  当然，你可以将字符串加在一起，或者更准确地说，将它们组合以形成更长的字符串：
  
  ```cpp
  #include <iostream>
  using namespace std;
  
  int main ()
  {
      string greet1 = "Hello";
      string greet2 = ", world!";
      string greet3 = greet1 + greet2;

      cout << greet3 << "\n";
  }
  ```
  
  ![](img/4aefeb2d095f688b34af6207870c5f39_56_2.png)

- **步骤 8**
  
  正如你所料，你可以混入一个整数并存储与字符串相关的某些内容。在这个例子中，我们创建了 `int length`，它存储了 `string.size()` 的结果并将其输出给用户：
  
  ```cpp
  #include <iostream>
  using namespace std;
  
  int main ()
  {
      int length;
      string greet1 = "Hello";
      string greet2 = ", world!";
      string greet3 = greet1 + greet2;

      length = greet3.size();
      cout << "The length of the combined strings is: ";
      cout << length << "\n";
  }
  ```

- **步骤 9**
  
  使用 string 函数附带的可用操作，你可以操作字符串的内容。例如，要从字符串中删除字符，你可以使用：
  
  ```cpp
  #include <iostream>
  using namespace std;
  
  int main ()
  {
      string strg ("Here is a long sentence in a string.");

      cout << strg << "\n";
      strg.erase (10,5);
      cout << strg << "\n";

      strg.erase (strg.begin()+8);
      cout << strg << "\n";

      strg.erase (strg.begin()+9, strg.end()-9);
      cout << strg << "\n";
  }
  ```

- **步骤 10**
  
  花点时间玩玩这些数字（它们是字符串中的字符位置）是值得的。有时候，你无法确定是否正确，所以熟能生巧。查看截图以查看代码的结果。
  
  ![](img/4aefeb2d095f688b34af6207870c5f39_56_3.png)

## C++ 数学

编程在本质上是数学的，正如你可能预料的那样，它内置了进行相当激烈的数学运算的广阔空间。对于在代码中实现数学模型的人来说，C++ 有很多可提供的内容。它可以非常复杂，也可以相对简单。

### C++ = MC2

基本数学符号在 C++ 中与应用于大多数其他编程语言时相同。然而，通过使用 C++ 数学库，你還可以計算平方根、幂、三角函數等。

- **步骤 1**
  
  C++ 的数学运算遵循与学校教授的模式相同的原则，即乘法和除法优先于加法和减法。不过，你可以改变这一点。暂时，创建一个新文件并输入：
  
  ```cpp
  #include <iostream>
  using namespace std;

  int main ()
  {
      float numbers = 100;

      numbers = numbers + 10; // This adds 10 to the initial 100
      cout << numbers << "\n";

      numbers = numbers - 10; // This subtracts 10 from the new 110
      cout << numbers << "\n";
  }
  ```

- **步骤 2**
  
  虽然简单，但它确实能热身一下旧的数学肌肉。注意我们为 `numbers` 变量使用了 float。虽然你可以愉快地使用整数，但如果你突然开始使用小数，就需要根据所需的精度更改为 float 或 double。运行代码并查看结果。
  
  ![](img/4aefeb2d095f688b34af6207870c5f39_57_0.png)

- **步骤 3**
  
  乘法和除法可以这样应用：
  
  ```cpp
  #include <iostream>
  using namespace std;

  int main ()
  {
      float numbers = 100;

      numbers = numbers * 10; // This multiplies 100 by 10
      cout << numbers << "\n";

      numbers = numbers / 10; // And this divides 1000 by 10
      cout << numbers << "\n";
  }
  ```

- **步骤 4**
  
  同样，执行简单代码并查看结果。虽然没什么特别有趣的，但这是 C++ 数学的介绍。我们在这里使用了 float，所以你可以玩弄代码，不仅可以乘以小数位，还可以进行除法、加法和减法。
  
  ![](img/4aefeb2d095f688b34af6207870c5f39_57_1.png)

![](img/4aefeb2d095f688b34af6207870c5f39_58_0.png)

- **步骤 5**
  
  当你调用 C++ 数学库时，就会出现有趣的数学内容。在这个头文件中，有数十个数学函数以及更多的操作。从计算余弦到双参数反正切，再到圆周率 Pi 的值。你可以这样调用该头文件：
  
  ```cpp
  #include <iostream>
  #include <cmath>
  using namespace std;

  int main ()
  {
      
  }
  ```
  
  ![](img/4aefeb2d095f688b34af6207870c5f39_58_1.png)

- **步骤 6**
  
  从获取数字的平方根开始：
  
  ```cpp
  #include <iostream>
  #include <cmath>
  using namespace std;

  int main ()
  {
      float number = 134;
      
      cout << "The square root of " << number << " is: " << sqrt(number) << "\n";
  }
  ```

- **步骤 7**
  
  在这里，我们创建了一个名为 `number` 的新 float，并使用 `sqrt(number)` 函数显示 134（变量 number 的值）的平方根。构建并运行代码，你的答案读取为 11.5758。
  
  ![](img/4aefeb2d095f688b34af6207870c5f39_58_5.png)
  
  ![](img/4aefeb2d095f688b34af6207870c5f39_58_6.png)
  
  ![](img/4aefeb2d095f688b34af6207870c5f39_58_7.png)

- **步骤 8**
  
  计算数字的幂可以通过以下方式完成：
  
  ```cpp
  #include <iostream>
  #include <cmath>
  using namespace std;

  int main ()
  {
      float number = 12;
      
      cout << number << " to the power of 2 is " << pow(number, 2) << "\n";
      cout << number << " to the power of 3 is " << pow(number, 3) << "\n";
      cout << number << " to the power of 0.8 is " << pow(number, 0.8) << "\n";
  }
  ```
  
  ![](img/4aefeb2d095f688b34af6207870c5f39_58_2.png)

- **步骤 9**
  
  在这里，我们创建了一个值为 12 的名为 `number` 的 float，而 `pow(变量, 幂)` 是发生计算的地方。当然，你不需要使用变量也可以计算幂和平方根。例如，`pow(12, 2)` 输出的值与代码中第一行 cout 相同。
  
  ![](img/4aefeb2d095f688b34af6207870c5f39_58_3.png)
  
  ![](img/4aefeb2d095f688b34af6207870c5f39_58_4.png)

- **步骤 10**
  
  圆周率 Pi 的值也存储在 cmath 头文件库中。可以使用 `M_PI` 函数调出它。在代码中进入 `cout << M_PI;`，你会得到 3.14159；或者你可以用它来计算：
  
  ```cpp
  #include <iostream>
  #include <cmath>
  using namespace std;

  int main ()
  {
      double area, radius = 1.5;
      
      area = M_PI * radius * radius;
      
      cout << area << "\n";
  }
  ```

