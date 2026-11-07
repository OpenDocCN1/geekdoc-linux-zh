```
```csharp
}

// 这个方法是不安全的，因为它要访问非托管内存
private unsafe static void DisplaySecureString(SecureString ss) {
    Char* pc = null;
    try {
        // 将 SecureString 解密到一个非托管内存缓冲区中
        pc = (Char*) Marshal.SecureStringToCoTaskMemUnicode(ss);

        // 访问包含已解密 SecureString 的非托管内存缓冲区
        for (Int32 index = 0; pc[index] != 0; index++)
            Console.Write(pc[index]);
    }
    finally {
        // 确定清零并释放包含已解密 SecureString 字符的非托管内存缓冲区
        if (pc != null)
            Marshal.ZeroFreeCoTaskMemUnicode((IntPtr) pc);
    }
}

}
```
```

System.Runtime.InteropServices.Marshal 类提供了 5 个方法来将一个 SecureString 的字符解密到非托管内存缓冲区。所有方法都是静态方法，所有方法都接受一个 SecureString 参数，而且所有方法都返回一个 IntPtr。每个方法都另有一个配对的方法，必须调用配对方法来清零并释放内部缓冲区。表 14-4 总结了 System.Runtime.InteropServices.Marshal 类提供的将 SecureString 解密到内部缓冲区的方法以及对应的清零和释放缓冲区的方法。

表 14-4 Marshal 类提供的用于操纵安全字符串的方法

| 将 SecureString 解密到缓冲的方法 | 清零并释放缓冲区的方法 |
|---|---|
| SecureStringToBSTR | ZeroFreeBSTR |
| SecureStringToCoTaskMemAnsi | ZeroFreeCoTaskMemAnsi |
| SecureStringToCoTaskMemUnicode | ZeroFreeCoTaskMemUnicode |
| SecureStringToGlobalAllocAnsi | ZeroFreeGlobalAllocAnsi |
| SecureStringToGlobalAllocUnicode | ZeroFreeGlobalAllocUnicode |