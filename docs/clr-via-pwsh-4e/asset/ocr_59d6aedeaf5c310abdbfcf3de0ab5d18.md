```
```csharp
[Serializable]
public class List<T> : IList<T>, ICollection<T>, IEnumerable<T>,
    IList, ICollection, IEnumerable {

    public List();
    public void Add(T item);
    public Int32 BinarySearch(T item);
    public void Clear();
    public Boolean Contains(T item);
    public Int32 IndexOf(T item);
    public Boolean Remove(T item);
    public void Sort();
    public void Sort(IComparer<T> comparer);
    public void Sort(Comparison<T> comparison);
    public T[] ToArray();

    public Int32 Count { get; }
    public T this[Int32 index] { get; set; }
}
```
```

泛型 List 类的设计者紧接在类名后添加了一个<T>，表明它操作的是一个未指定的数据类型。定义泛型类型或方法时，为类型指定的任何变量(比如 T)都称为类型参数(type parameter)。T 是变量名，源代码能使用数据类型的任何地方都能使用 T。例如，在 List 类定义中，T 被用于方法参数(Add 方法接受一个 T 类型的参数)和返回值(ToArray 方法返回 T 类型的一维数组)。另一个例子是索引器方法(在 C#中称为 this)。索引器有一个 get 访问器方法，它返回 T 类型的值；一个 set 访问器方法，它接受 T 类型的参数。由于凡是能指定一个数据类型的地方都能使用 T 变量，所以在方法内部定义一个局部变量时，或者在类中定义字段时，也可以使用 T。

> 注意 根据 Microsoft 的设计原则，泛型参数变量要么称为 T，要么至少以大写 T 开头(如 TKey 和 TValue)。大写 T 代表类型(Type)，就像大写 I 代表接口(Interface)一样，比如 IComparable。

定义好泛型 List<T>类型之后，其他开发人员为了使用这个泛型算法，要指定由算法操作的具体数据类型。使用泛型类型或方法时指定的具体数据类型称为类型实参(type argument)。例如，开发人员可指定一个 DateTime 类型实参来使用 List 算法。以下代码对此进行了演示：

```
```csharp
private static void SomeMethod() {
    // 构造一个 List 来操作 DateTime 对象
    List<DateTime> dtList = new List<DateTime>();

    // 向列表添加一个 DateTime 对象
    dtList.Add(DateTime.Now);                  // 不进行装箱

    // 向列表添加另一个 DateTime 对象
    dtList.Add(DateTime.MinValue);             // 不进行装箱

    // 尝试向列表中添加一个 String 对象
    dtList.Add("1/1/2004");                    // 编译时错误

    // 从列表提取一个 DateTime 对象
    DateTime dt = dtList[0];                   // 不需要转型
}
```
```