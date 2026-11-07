```
Appointment[] appointments = GetAppointmentsForToday();
if (appointments != null) {
    for (Int32 a = 0, a < appointments.Length; a++) {
        // 对 appointments[a] 执行操作
    }
}
```

将方法设计为返回对含有 0 个元素的一个数组的引用，而不是返回 null，该方法的调用者就能更轻松地使用该方法。顺便提一句，对字段也应如此。如果类型中有一个字段是数组引用，应考虑让这个字段始终引用数组，即使数组中不包含任何元素。

# 16.6 创建下限非零的数组

前面提到过，能创建和操作下限非 0 的数组。可以调用数组的静态 **CreateInstance** 方法来动态创建自己的数组。该方法有若干个重载版本，允许指定数组元素的类型、数组的维数、每一维的下限和每一维的元素数目。**CreateInstance** 为数组分配内存，将参数信息保存到数组的内存块的开销(overhead)部分，然后返回对该数组的引用。如果数组维数是 2 或 2 以上，就可以把 **CreateInstance** 返回的引用转型为一个 **ElementType[][]** 变量(**ElementType** 要替换为类型名称)，以简化对数组中的元素的访问。如果只有一维，C#要求必须使用该 **Array** 的 **GetValue** 和 **SetValue** 方法访问数组元素。

以下代码演示了如何动态创建由 **System.Decimal** 值构成的二维数组。第一维代表 2005 到 2009(含)年份，第二维代表 1 到 4(含)季度。代码遍历动态数组中的所有元素。我本来可以将数组的上限硬编码到代码中，这样能获得更好的性能。但我最后决定使用 **System.Array** 的 **GetLowerBound** 和 **GetUpperBound** 方法来演示它们的用法：

```
using System;

public sealed class DynamicArrays {
    public static void Main() {
        // 我想创建一个二维数组 (2005..2009)[1..4]
        Int32[] lowerBounds = { 2005, 1 };
        Int32[] lengths = { 5, 4 };
        Decimal[,] quarterlyRevenue = (Decimal[,])
            Array.CreateInstance(typeof(Decimal), lengths, lowerBounds);

        Console.WriteLine("{0,4} {1,9} {2,9} {3,9} {4,9}",
            "Year", "Q1", "Q2", "Q3", "Q4");
        Int32 firstYear = quarterlyRevenue.GetLowerBound(0);
        Int32 lastYear = quarterlyRevenue.GetUpperBound(0);
        Int32 firstQuarter = quarterlyRevenue.GetLowerBound(1);
        Int32 lastQuarter = quarterlyRevenue.GetUpperBound(1);

        for (Int32 year = firstYear; year <= lastYear; year++) {
            Console.Write(year + " ");
            for (Int32 quarter = firstQuarter; quarter <= lastQuarter; quarter++) {
                Console.Write("{0,9:C} ", quarterlyRevenue[year, quarter]);
            }
            Console.WriteLine();
        }
    }
}
```