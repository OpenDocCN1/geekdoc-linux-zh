
完成。在第 26 到 29 行创建了四个类：`xTooBig`、`xTooSmall`、`xZero` 和 `xNegative`。在构造函数第 56 到 71 行中，检查传递给构造函数的 `size`。如果它太大、太小或为零，则抛出异常。`try` 块被改为包含除负以外的每个条件的 `catch`，这由第 104 行的“捕获所有”语句 `catch(...)` 捕获。当 `size` 为 -5 时，你可能期望调用 `xNegative`，但构造函数中的顺序（`size < 10`）阻止了这一点。要修复这个问题，请交换第 61 和 62 行并重新编译。

# 异常层次结构

异常是类，因此它们可以派生。创建一个 `xSize` 类并让 `xTooSmall`、`xTooBig`、`Negative` 派生自它是有利的。这样，某些函数可以捕获 `xSize` 异常，而其他函数可以捕获特定类型的 `xSize` 异常。列表 20.3 展示了这一思想。

## 列表 20.3 异常层次结构与异常

```cpp
1: #include <iostream.h>
2: // Listing 20.3: Class Hierarchies and Exceptions
3: const int DefaultSize = 10;
4: 
5: class Array
6: {
7:  public:
8:     // constructors
9:     Array(int textSize = DefaultSize);
10:    Array(const Array& rhs);
11:    ~Array() { delete [] pType; }
12: 
13:    // operators
14:    Array& operator=(const Array&);
15:    int& operator[](int offset);
16:    const int operator[](int offset) const;
17: 
18:    // accessors
19:    int GetSize() const { return textSize; }
20: 
21:    // friend function
22:    friend ostream& operator<<(ostream&, const Array);
23: 
24:    // define the exception classes
25:    class xBoundary {};
26:    class xSize {};
27:    class xTooBig : public xSize {};
28:    class xSmall : public xSize {};
29:    class xZero : public xSmall {};
30:    class xNegative : public xSize {};
31:    private:
32:    int *pType;
33:    int itsSize;
34:    }
35: 
36: 
37:    Array::Array(int size):
38:        itsSize(size)
39:    {
40:        if (size == 0)
41:            throw xZero();
42:        if (size > 30000)
43:            throw xTooBig();
44:        if (size < 1)
45:            throw xNegative();
46:        if (size < 10)
47:            throw xTooSmall();
48: 
49:        pType = new int[size];
50:        for (int i = 0; i<size; i++)
51:            pType[i] = 0;
52:    }
53: 
54:    int& Array::operator[](int offset) const
55:    {
56:        int size = GetItsSize();
57:        if (offset >= 0 && offset < GetItsSize())
58:            return pType[offset];
59:        throw xBoundary();
60:        return pType[0]; // appease MFC
61:    }
62: 
63:    int main()
64:    {
65:
66:        try
67:        {
68:            Array(0);
69:            for (int j = 0; j < 100; j++)
70:            {
71:                intArray[j] = j;
72:                cout << "intArray[" << j << "] okay...\n";
73:            }
74:        }
75:        catch (Array::xBoundary)
76:        {
77:            cout << "Unable to process your input!\n";
78:        }
79:        catch (Array::xTooBig)
80:        {
81:            cout << "This array is too big...\n";
82:        }
83:        catch (Array::xTooSmall)
84:        {
85:            cout << "This array is too small...\n";
86:        }
87:        catch (Array::xZero)
89:        {
90:            cout << "You asked for an array of objects!\n";
91:        }
92:        catch (...)
93:        {
94:            cout << "Something wrong!\n";
95:        }
96:        cout << "Done.\n";
97:        return 0;
98:    }
```

## 列表 20.3（续）

```cpp
105:     catch (...)
106:     {
107:         cout << "Something went wrong!\n";
108:     }
109:     cout << "Done.\n";
110:     return 0;
111:     }
```

# 输出

此数组太小了...
Done.

# 分析

重要的变化位于第 27 到 30 行，那里建立了类层次结构。类 `xToBig`、`xToSmall` 和 `xNegative` 派生自 `xSize`，而 `xZero` 派生自 `xToSmall`。

数组按大小为 0 创建，但发生了什么？似乎捕获到了错误的异常！仔细检查 `catch` 块，你会发现它在查找类型为 `xZero` 的异常之前，先查找类型为 `xToSmall` 的异常。因为抛出的是 `xZero` 对象而它是 `xToSmall` 的，所以它被 `xToSmall` 的处理器捕获了。异常被处理后，它不会传递给其他处理器，因此 `xZero` 的处理器永远不会被调用。

解决问题的方法是仔细排列处理器的顺序，使得最特定的处理器在前，较不特定的处理器在后。在这个特定的示例中，通过交换 `xZero` 和 `xToSmall` 两个处理器的位置即可解决问题。

# 通过命名异常对象访问异常中的数据

你通常想知道不仅仅是抛出了什么类型的异常，以便对错误做出正确响应。异常类与其他任何类相同。你可以自由地提供数据、在构造函数中初始化数据并在任何时候读取这些数据。列表 20.4 显示了如何这样做。

```cpp
1:     #include <iostream>
2:     // 包含列表 20.4：获取异常对象数据
3:     const int DefaultSize = 10;
4: 
# 异常与错误处理

```cpp
5:   class Array 
6:   {
7:   public:
8:     // 构造函数
9:     Array(int intSize = DefaultSize);
10:    Array(const Array &rhs);
11:    ~Array() { delete [] pType;}
12:
13: 
14:    // 运算符
15:    Array& operator=(const Array&);
16:    int& operator[](int intOffset);
17:    const int& operator[](int intOffset) const;
18:
19:    // 访问器
20:    int GetSize() const { return itsSize; }
21:
22:    // 友元函数
23:    friend ostream& operator<<(ostream&, const Array&);
24:
25:    // 定义异常类
26:    class xBoundary {};
27:    class xSize
28:    {
29:      public:
30:        xSize(int size):itsSize(size) {}
31:        ~xSize() {}
32:        int GetSize() { return itsSize; }
33:      private:
34:        int itsSize;
35:      };
36:
37:    class xTooBig : public xSize
38:    {
39:      public:
40:        xTooBig(int size):xSize(size){}
41:      };
42:
43:    class xTooSmall : public xSize
44:    {
45:      public:
46:        xTooSmall(int size):xSize(size){}
47:      };
48:
49:    class xZero : public xTooSmall
50:    {
51:      public:
52:        xZero(int size):xTooSmall(size){}
53:      };
54:
55:    class xNegative : public xSize
56:    {
57:    public:
58:        xNegative(int size):xSize(size){
59:    }
60:
61:    private:
62:        int *pType;
63:        int itsSize;
64:    }
65:
66:
66:    Array(int size):
67:        itsSize(size)
68:    {
69:        if (size == 0)
70:            throw xZero(size);
71:        if (size > 30000)
72:            throw xTooBig(size);
73:        if (size < 1)
74:            throw xNegative(size);
75:        if (size < 10)
76:            throw xTooSmall(size);
77:
78:        pType = new int[size];
79:        for (int i = 0; i<size; i++)
80:            pType[i] = 0;
81:    }
82:
83:
84:int& Array::operator[](int offset)
85:    {
86:        int size = GetSize();
87:        if (offset >= 0 && offset < GetSize())
88:            return pType[offset];
89:        throw xOutBoundary();
90:        return pType[0];
91:    }
```

# 列表 20.5 继续

```cpp
79:    virtual void PrintError()
80:    {
81:        cout << "Negative! Received: *";
82:        cout << xSize::itsSize << endl;
83:
84:    }
85:
86:    private:
87:        int *pType;
88:        int itsSize;
89:    };
90:
91:    Array::Array(int size):
92:        itsSize(size)
93:    {
94:        if (size == 0)
95:            throw xZero(size);
96:
97:        if (size > 30000)
98:            throw xTooBig(size);
99:
100:       if (size < 1)
101:           throw xNegative(size);
102:       if (size < 10)
103:           throw xTooSmall(size);
104:
105:    pType = new int[size];
106:    for (int i = 0; i<size; i++)
107:        pType[i] = 0;
108:    }
109:
110:   int& Array::operator[](int offset)
111:    {
112:        int size = GetSize();
113:        if (offset >= 0 && offset < GetSize())
114:            return pType[offset];
115:        throw xBoundary();
116:        return pType[0];
117:    }
118:
119:   const int& Array::operator[](int offset) const
120:    {
121:        int size = GetSize();
122:        if (offset >= 0 && offset < GetSize())
123:            return pType[offset];
124:        throw xBoundary();
125:        return pType[0];
126:    }
127:
128:   int main()
```

# 异常与错误处理

```cpp
127:  {
128:    try
129:      Array intArray(9);
130:      for (int j = 0; j < 100; j++)
131:      {
132:        intArray[j] = j;
133:        cout << "intArray[" << j << " "] okay...\n";
134:      }
135:    }
136:  catch (Array::xBoundary)
137:    {
138:      cout << "Unable to process your input!\n";
139:    }
140:  catch (Array::xSize& theException)
141:    {
142:      theException.PrintError();
143:    }
144:  catch (...)
145:    {
146:      cout << "Something went wrong!\n";
147:    }
148:  cout << "Done.\n";
149:  return 0;
150: }
```

太小了！接收到：9

完成。

列表 20.5 在 `xClass` 中声明了一个虚函数方法 `PrintError()`，该方法会打印错误信息和类的实际大小。该方法在每个派生类中都被重写了。

在第 142 行，异常对象被声明为引用。当通过引用调用 `PrintError()` 时，多态性会调用 `PrintError()` 的正确版本。这种代码更整洁、更易理解，且更于维护。

# 使用异常与模板

在创建用于配合模板的异常时，你会有两种选择：你可以为模板的每个实例创建一个异常，也可以使用在模板声明之外声明的异常类。列表 20.6 演示了这两种方法。

# 输入 列表 20.6 在模板中使用异常
