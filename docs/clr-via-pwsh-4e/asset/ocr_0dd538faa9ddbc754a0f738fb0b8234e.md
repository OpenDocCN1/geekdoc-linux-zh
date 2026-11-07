**重要提示**  一些开发人员可能注意到 **System.AppDomain** 提供了 **Load** 方法。和 **Assembly** 的静态 **Load** 方法不同，**AppDomain** 的 **Load** 是实例方法，它允许将程序集加载到指定的 **AppDomain** 中。该方法设计由非托管代码调用，允许宿主将程序集“注入”特定 **AppDomain** 中。托管代码的开发人员一般情况下不应调用它，因为调用 **AppDomain** 的 **Load** 方法时需要传递一个标识了程序集的字符串。该方法随后会应用策略，并在一些常规位置搜索程序集。我们知道，AppDomain 关联了一些告诉 CLR 如何查找程序集的设置。为了加载这个程序集，CLR 将使用与指定 AppDomain 关联的设置，而非与发出调用之 AppDomain 关联的设置。

但 **AppDomain** 的 **Load** 方法会返回对程序集的引用。由于 **System.Assembly** 类不是从 **System.MarshalByRefObject** 派生的，所以程序集对象必须按值封送回发出调用的那个 **AppDomain**。但是，现在 CLR 就会用发出调用的那个 **AppDomain** 的设置来定位并加载程序集。如果使用发出调用的那个 **AppDomain** 的策略和搜索位置找不到指定的程序集，就会抛出一个 **FileNotFoundException**。这个行为一般不是你所期望的，所以应该避免使用 **AppDomain** 的 **Load** 方法。

在大多数动态可扩展应用程序中，**Assembly** 的 **Load** 方法是将程序集加载到 **AppDomain** 的首选方式。但它要求事先掌握构成程序集标识的各个部分。开发人员经常需要写一些工具或实用程序(例如 ILDasm.exe, PEVerify.exe, CorFlags.exe, GACUtil.exe, SGen.exe, SN.exe 和 XSD.exe 等)来操作程序集，它们都要获取引用了程序集文件路径名(包括文件扩展名)的命令行实参。

调用 **Assembly** 的 **LoadFrom** 方法加载指定了路径名的程序集：

```
```csharp
public class Assembly {
    public static Assembly LoadFrom(String path);
    // 未列出不常用的 LoadFrom 重载
}
```
```

在内部，**LoadFrom** 首先调用 **System.Reflection.AssemblyName** 类的静态 **GetAssemblyName** 方法。该方法打开指定的文件，找到 **AssemblyRef** 元数据表的记录项，提取程序集标识信息，然后以一个 **System.Reflection.AssemblyName** 对象的形式返回这些信息(文件同时会关闭)。随后，**LoadFrom** 方法在内部调用 **Assembly** 的 **Load** 方法，将 **AssemblyName** 对象传给它。然后，CLR 应用版本绑定重定向策略，并在各个位置查找匹配的程序集。**Load** 找到匹配程序集会加载它，并返回代表已加载程序集的 **Assembly** 对象；**LoadFrom** 方法将返回这个值。如果 **Load** 没有找到匹配的程序集，**LoadFrom** 会加载通过 **LoadFrom** 的实参传递的路径中的程序集。当然，如果已加载了具有相同标识的程序集，**LoadFrom** 方法就会直接返回代表已加载程序集的 **Assembly** 对象。

顺便说一句，**LoadFrom** 方法允许传递一个 URL 作为实参，下面是一个例子：