```
```csharp
using System.Linq;

// 下面是一些不同的委托定义
internal delegate Object TwoInt32s(Int32 n1, Int32 n2);
internal delegate Object OneString(String s1);

public static class DelegateReflection {
   public static void Main(String[] args) {
      if (args.Length < 2) {
         String usage =
            "Usage:" +
            "{0} delType methodName [Arg1] [Arg2]" +
            "{0}    where delType must be TwoInt32s or OneString" +
            "{0}    if delType is TwoInt32s, methodName must be Add or Subtract" +
            "{0}    if delType is OneString, methodName must be NumChars or Reverse"+
            "{0}" +
            "{0}Examples:" +
            "{0}    {1} TwoInt32s Add 123 321" +
            "{0}    {1} TwoInt32s Subtract 123 321" +
            "{0}    {1} OneString NumChars (\"Hello there\")" +
            "{0}    {1} OneString Reverse (\"Hello there\")";
         Console.WriteLine(usage, Environment.NewLine);
         return;
      }

      // 将 delType 实参转换为委托类型
      Type delType = Type.GetType(args[0]);
      if (delType == null) {
         Console.WriteLine("Invalid delType argument: " + args[0]);
         return;
      }

      Delegate d;
      try {
         // 将 Arg1 实参转换为方法
         MethodInfo mi =
            typeof(DelegateReflection).GetTypeInfo().GetDeclaredMethod(args[1]);

         // 创建包装了静态方法的委托对象
         d = mi.CreateDelegate(delType);
      }
      catch (ArgumentException) {
         Console.WriteLine("Invalid methodName argument: " + args[1]);
         return;
      }

      // 创建一个数组，其中只包含要通过委托对象传给方法的参数
      Object[] callbackArgs = new Object[args.Length - 2];

      if (d.GetType() == typeof(TwoInt32s)) {
         try {
            // 将 String 类型的参数转换为 Int32 类型的参数
            for (Int32 a = 2; a < args.Length; a++)
               callbackArgs[a - 2] = Int32.Parse(args[a]);
         }
         catch (FormatException) {
            Console.WriteLine("Parameters must be integers.");
            return;
         }
      }

      if (d.GetType() == typeof(OneString)) {
         // 只复制 String 参数
         Array.Copy(args, 2, callbackArgs, 0, callbackArgs.Length);
      }
```
```