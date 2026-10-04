
# 模板特化示例

## 程序输出

```text
Please use values between 0 and 9****

Enter an offset (0-9) and a value. (-1 to stop): -1 -1

intArray...
[0] 0
[1] 10

[2] 20
[3] 30
[4] 40
[5] 50
[6] 60
[7] 70
[8] 80
[9] 90

animalArray:...

[0] 0
[1] 100
[2] 200
[3] 300
[4] 400
[5] 500
[6] 600
[7] 700
[8] 800
[9] 900
```

## 代码分析

为了节省空间，省略了 `Array` 类的大部分实现。`Animal` 类在第 6–23 行定义。虽然这是一个精简的类，但它提供了自己的插入运算符（`<<`）来允许打印动物。打印只是显示了动物的当前重量。

注意 `Animal` 有一个默认构造函数。这是必要的，因为当你将对象添加到数组时，会使用对象的默认构造函数来创建对象。这产生了一些困难，正如你所看到的。

在第 101 行，声明了函数 `IntFillFunction()`。原型表明该函数接收一个整数数组。请注意这不是一个模板函数。`IntFillFunction()` 只期望一种类型的数组——整数数组。同样，在第 102 行，`AnimalFillFunction()` 被声明为接收 `Animal` 数组。

### 特殊化函数

如果你取消列表 19.5 中构造函数（第 36 和 42 行）和析构函数（第 47 行）中的 `cout` 语句，你就可以看到动物意外的构造和析构。

当对象被添加到数组时，会调用默认构造函数。然而，`Array` 构造函数会为数组的每个成员赋值，如列表 19.2 第 59 和 60 行所示。

这是一个不幸的时间浪费，因为你不能删除这一行，因为整数不会自动初始化为值。解决方案是告诉模板不要使用这个构造函数，而是使用一个特殊的构造函数。

你可以为 `Animal` 类提供一个显式的实现，如列表 19.6 所示。

```cpp
Animal::Animal(int weight)
    : itsWeight(weight)
{
    cout << "animal" << (int)weight;
}

Animal::Animal()
    : itsWeight(0)
{
    cout << "animal";
}

Animal::~Animal()
{
    cout << "Destroyed an animal...";
}

template <class T> // 模板和参数
class Array
{
public:
    Array(int size = DefaultSize);
    Array(const Array& rhs);
    ~Array() { delete [] pType; }

    // 运算符
    Array& operator=(const Array&);
    T& operator[](int offset) { return pType[offset]; }
    const T& operator[](int offset) const
        return pType[offset];

    // 访问器
    int GetSize() const { return itsSize; }

    // 友元函数
    friend ostream& operator<<(ostream&, const Array<T>);

private:
    T *pType;
    int itsSize;
};

template <class T>
Array::Array(int size = DefaultSize)
    : itsSize(size)
{
    pType = new T[size];
    for (int i = 0; i < size; i++)
        pType[i] = (T)0;
}

template <class T>
// 列表 19.6 继续
Array<T>& Array<T>::operator=(const Array& rhs)
{
    if (this == &rhs)
        return *this;
    delete [] pType;
    itsSize = rhs.GetSize();
    pType = new T[itsSize];
    for (int i = 0; i < itsSize; i++)
        pType[i] = rhs[i];
    return *this;
}

template <class T>
Array<T>::Array(const Array& rhs)
{
    itsSize = rhs.GetSize();
    pType = new T[itsSize];
    for (int i = 0; i < itsSize; i++)
        pType[i] = rhs[i];
}

template <class T>
ostream& operator<<(ostream& output, const Array<T>& array)
{
    for (int i = 0; i < array.GetSize(); i++)
        output << "[" << i << "]" << array[i] << endl;
    return output;
}

Array<Animal>::Array(int AnimalSize)
    : itsSize(AnimalSize)
{
    pType = new Animal[AnimalSize];
}

void IntFillFunction(Array<int>& array);
void AnimalFillFunction(Array<Animal>& array);

int main()
{
    Array<int> intArray;
    Array<Animal> animalArray;
    IntFillFunction(intArray);
    AnimalFillFunction(animalArray);
    cout << "\intArray...\n" << intArray;
    cout << "\nanimalArray...\n" << animalArray << endl;
    return 0;
}

void IntFillFunction(Array<int>& array)
{
    bool Stop = false;
    int offset, value;
    while (!Stop)
    {
        cout << "****输入一个偏移量 (0-9)****和一个值.";
        cout << "-1退出: ";
        cin >> offset >> value;
        if (offset < 0)
            break;
        if (offset > 9)
        {
            cout << "****请使用0到9之间的值****";
            continue;
        }
        array[offset] = value;
    }
}

void AnimalFillFunction(Array<Animal>& array)
{
    Animal *pAnimal;
    for (int i = 0; i < array.GetSize(); i++)
    {
        pAnimal = new Animal(i);
        array[i] = *pAnimal;
        delete pAnimal;
    }
}
```

## 模板 685

输出中增加了行号以便分析。你的输出中不会显示行号。

- 1: animal(0) 输入一个偏移量 (0-9)和一个值。 (-1退出): 0 0
- 2: 输入一个偏移量 (0-9)和一个值。 (-1退出): 1 1
- 3: 输入一个偏移量 (0-9)和一个值。 (-1退出): 2 2
- 4: 输入一个偏移量 (0-9)和一个值。 (-1退出): 3 3
- 5: 输入一个偏移量 (0-9)和一个值。 (-1退出): -1 -1
- 6: animal(int) 销毁了一个动物...animal(int) 销毁了一个动物...animal(int) 销毁了一个动物...init... [0] 0
- 7: [1] 1
- 8: [2] 2
- 9:  array...
- 10: [0] 10
- 11: [1] 10
- 12: [2] 20
- 13: 销毁了一个动物...销毁了一个动物...销毁了一个动物...
- 14: 第二次运行
- 15: animal(int) 销毁了一个动物...
- 16: animal(int) 销毁了一个动物...
- 17: animal(int) 销毁了一个动物...
- 18: 输入一个偏移量 (0-9)和一个值。 (-1退出): 0 0
- 19: 输入一个偏移量 (0-9)和一个值。 (-1退出): 1 1
- 20: 输入一个偏移量 (0-9)和一个值。 (-1退出): 2 2
- 21: 输入一个偏移量 (0-9)和一个值。 (-1退出): 3 3
- 22: animal(int) 销毁了一个动物...
- 23: animal(int) 销毁了一个动物...
- 24: animal(int) 销毁了一个动物...
- 25: init...
- 26: [0] 0
- 27: [1] 1
- 28: [2] 2

## 模板代码片段

```cpp
61:   T& operator[](int offset) { return pType[offset]; }
62:   const T& operator[](int offset) const
63:   { return pType[offset]; }
64:   // 访问器
65:   int GetSize() const { return itsSize; }
66:   static int getNumberArrays() { return itsNumberArrays; }
67:   
68:   // 友元函数
69:   friend ostream& operator<< <> (ostream&, const Array<T>&);
70:   
71:   private:
72:       T *pType;
73:       int itsSize;
74:       static int itsNumberArrays;
75:   };

77:   template <class T>
78:   int Array<T>::itsNumberArrays = 0;

80:   template <class T>
81:   Array<T>::Array(int size = DefaultSize):
82:   itsSize(size)
83:   {
84:       pType = new T[size];
85:       for (int i = 0; i<size; i++)
86:           pType[i] = (T)0;
87:           itsNumberArrays++;
88:   }

90:   template <class T>
91:   Array<T>& Array<T>::operator=(const Array &rhs)
92:   {
93:       if (this == &rhs)
94:           return *this;
95:           delete [] pType;
96:           itsSize = rhs.GetSize();
97:           pType = new T[itsSize];
98:           for (int i = 0; i<itsSize; i++)
99:               pType[i] = rhs[i];
100:  }

template <class T>

101:  Array<T>::Array(const Array &rhs)
102:  {
103:      itsSize = rhs.GetSize();
104:      pType = new T[itsSize];
105:      for (int i = 0; i<itsSize; i++)
106:          pType[i] = rhs[i];
107:          itsNumberArrays++;
108:  }
```

### 列表 19.7 续

```cpp
112:   template <class T>
113:   ostream& operator<< (ostream& output, const Array<T>& theArray)
114: {
116:     for (int i = 0; i<theArray.GetSize(); i++)
117:       output << "[" << i << "]" << theArray[i] << endl;
118:     return output;
119: }

123:   int main()
124:   {
126:     cout << Array<int>::GetNumberArrays() << " integer arrays\n";
127:     cout << Array<Animal>::GetNumberArrays();
128:     cout << " animal arrays\n";
129:     Array<int> intArray;
130:     Array<Animal> animalArray;
132:     cout << intArray.GetNumberArrays() << " integer arrays\n";
133:     cout << animalArray.GetNumberArrays();
134:     cout << " animal arrays\n";
136:     Array<int>* pIntArray = new Array<int>;
138:     cout << Array<int>::GetNumberArrays() << " integer arrays\n";
139:     cout << Array<Animal>::GetNumberArrays();
140:     cout << " animal arrays\n";
142:     delete pIntArray;
144:     cout << Array<int>::GetNumberArrays() << " integer arrays\n";
145:     cout << Array<Animal>::GetNumberArrays();
146:     cout << " animal arrays\n";
147:     return 0;
148: }
```
