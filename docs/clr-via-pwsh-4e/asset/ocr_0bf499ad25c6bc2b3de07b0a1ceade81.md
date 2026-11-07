```
```csharp
output += String.Format("Simple {0} Compare: {1} {3} {2}",
    ci.Name, s1, s2, symbol[x + 1]);
output += Environment.NewLine;

// 以下是忽略日语假名的比较结果
CompareInfo compareInfo = CompareInfo.GetCompareInfo("ja-JP");
x = Math.Sign(compareInfo.Compare(s1, s2, CompareOptions.IgnoreKanaType));
output += String.Format("Advanced {0} Compare: {1} {3} {2}",
    ci.Name, s1, s2, symbol[x + 1]);

MessageBox.Show(output, "Comparing Strings For Sorting");
}
}
```
```

生成并运行以上代码得到如图 14-1 所示的结果。

![](bbox=[0.365, 0.291, 0.672, 0.432])

图 14-1  字符串排序结果

> **注意①** 源代码不要用 ANSI 格式保存，否则日语字符会丢失。要在 Microsoft Visual Studio 中保存这个文件，请打开“另存文件为”对话框，单击“保存”按钮右侧的下箭头，选择“编码保存”，并选择“Unicode (UTF-8 带签名)-代码页 65001”。Microsoft C#编译器用这个代码页就能成功解析源代码文件了。

除了 **Compare**，**CompareInfo** 类还提供了 **IndexOf**，**LastIndexOf**，**IsPrefix** 和 **IsSuffix** 方法。由于所有这些方法都提供了接受 **CompareOptions** 枚举值的重载版本，所以能提供比 **String** 类定义的 **Compare**，**IndexOf**，**LastIndexOf**，**StartsWith** 和 **EndsWith** 方法更全面的控制。另外，FCL 的 **System.StringComparer** 类也能执行字符串比较，它适合对大量不同的字符串反复执行同一种比较。

# 14.2.4  字符串留用

如上一节所述，检查字符串相等性是应用程序的常见操作，也是一种可能严重损害性能的操作。执行序号(ordinal)相等性检查时，CLR 快速测试两个字符串是否包含相同数量的字符。答案否定，字符串肯定不相等；答案肯定，字符串则可能相等。然后，CLR 必须比较