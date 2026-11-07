```
IL_0015: ldc.i4.0
IL_0016: ldloc.0
IL_0017: ldfld char Program/<>c__DisplayClass1::charToFind
IL_001c: box [mscorlib]System.Char
IL_0021: stelem.ref
IL_0022: ldloc.1
IL_0023: ldc.i4.1
IL_0024: ldstr ": "
IL_0029: stelem.ref
IL_002a: ldloc.1
IL_002b: ldc.i4.2
IL_002c: ldarg.0
IL_002d: callvirt instance class [mscorlib]System.Type [mscorlib]System.Object::GetType()
IL_0032: stelem.ref
IL_0033: ldloc.1
IL_0034: ldc.i4.3
IL_0035: ldsfld string [mscorlib]System.String::Empty
IL_003a: stelem.ref
IL_003b: ldloc.1
IL_003c: ldc.i4.4
IL_003d: ldarg.0
IL_003e: callvirt instance int64 [mscorlib]System.IO.Stream::get_Position()
IL_0043: call valuetype [mscorlib]System.Decimal [mscorlib]System.Decimal::op_Implicit(int64)
IL_0048: ldc.i4 0x200
IL_004d: newobj instance void [mscorlib]System.Decimal::.ctor(int32)
IL_0052: call valuetype [mscorlib]System.Decimal [mscorlib]System.Decimal::op_Addition(valuetype [mscorlib]System.Decimal, valuetype [mscorlib]System.Decimal)
IL_0057: box [mscorlib]System.Decimal
IL_005c: stelem.ref
IL_005d: ldloc.1
IL_005e: call string [mscorlib]System.String::Concat(object[])
IL_0063: ldloc.0
IL_0064: ldftn instance bool Program/<>c__DisplayClass1::<OneStatement>b__0(char)
IL_006a: newobj instance void [mscorlib]System.Func`2<char, bool>::.ctor(object, native int)
IL_006f: call class [mscorlib]System.Collections.Generic.IEnumerable`1<!0> [System.Core]System.Linq.Enumerable::Where<char>(class [mscorlib]System.Collections.Generic.IEnumerable`1<!0>, class [mscorlib]System.Func`2<!0, bool>)
IL_0074: call !![0] [System.Core]System.Linq.Enumerable::ToArray<char>(class [mscorlib]System.Collections.Generic.IEnumerable`1<!0>)
IL_0079: ret
}
```

由此可见，构造<>c__DisplayClass1 类(编译器生成的类型)、Object[]数组和 Func 委托，以及对 char 和 Decimal 进行装箱时，可能抛出一个 OutOfMemoryException。调用 Concat，