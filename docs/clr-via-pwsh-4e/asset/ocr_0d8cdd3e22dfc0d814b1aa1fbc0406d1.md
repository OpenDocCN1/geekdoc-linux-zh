```
public void ProcessBytes(Stream someStream) { ... }

// 不好：方法使用强参数类型
public void ProcessBytes(FileStream fileStream) { ... }
```

第一个方法能处理任何流，包括 **FileStream**、**NetworkStream** 和 **MemoryStream** 等。第二个只能处理 **FileStream** 流，这限制了它的应用。

相反，一般最好是将方法的返回类型声明为最强的类型（防止受限于特定类型）。例如，方法最好返回 **FileStream** 而不是 **Stream** 对象：

```
// 好：方法使用强返回类型
public FileStream OpenFile() { ... }

// 不好：方法使用弱返回类型
public Stream OpenFile() { ... }
```

第一个方法是首选的，它允许方法的调用者将返回对象视为 **FileStream** 对象或者 **Stream** 对象。但第二个方法要求调用者只能将返回对象视为 **Stream** 对象。总之，要确保调用者在调用方法时有尽量大的灵活性，使方法的适用范围更大。

有时需要在不影响调用者的前提下修改方法的内部实现。在刚才的例子中，**OpenFile** 方法不太可能更改内部实现来返回除 **FileStream**（或 **FileStream** 的派生类型）之外的其他对象。但如果方法返回 **List<String>** 对象，就可能想在未来的某个时候修改它的内部实现来返回一个 **String[]**。如果想保持一定的灵活性，在将来更改方法返回的东西，请选择一个较弱的返回类型。例如：

```
// 灵活：方法使用较弱的返回类型
public IList<String> GetStringCollection() { ... }

// 不灵活：方法使用较强的返回类型
public List<String> GetStringCollection() { ... }
```

在这个例子中，即使 **GetStringCollection** 方法在内部使用一个 **List<String>** 对象并返回它，但最好还是修改方法的原型，使它返回一个 **IList<String>**。将来，**GetStringCollection** 方法可更改它的内部集合来使用一个 **String[]**。与此同时，不需要修改调用者的源代码。事实上，调用者甚至不需要重新编译。注意，这个例子在较弱的类型中选择的是最强的那一个。例如，它没有使用最弱的 **IEnumerable<String>**，也没有使用较强的 **ICollection<String>**。

# 9.6 常量性

有的语言（比如非托管 C++）允许将方法或参数声明为常量，从而禁止实例方法中的代码更改对象的任何字段，或者更改传给方法的任何对象。CLR 没有提供这个功能，许多程序员因此觉得很遗憾。既然 CLR 都不提供，面向它的任何编程语言（包括 C#）自然也无法提供。

① IList 继承自 ICollection，ICollection 继承自 IEnumerable。作者的意思是说，在这三个比 List<String> 都弱的类型中，选择的是最强的 IList。——译注