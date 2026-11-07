```
CodePage=65001, WindowsCodePage=1200
WebName=utf-8, HeaderName=utf-8, BodyName=utf-8
IsBrowserDisplay=True, IsBrowserSave=True
IsMailNewsDisplay=True, IsMailNewsSave=True
```

表 14-3 总结了 Encoding 的所有派生类都提供的常用方法。

# 表 14-3　Encoding 的派生类提供的方法

| 方法名称 | 说明 |
|---|---|
| GetPreamble | 返回一个字节数组，指出在写入任何已编码字节之前，首先应该在一个流中写入什么字节。这些字节经常称为“前导码”（preamble）或“字节顺序标记”（Byte Order Mark，BOM）字节。开始从一个流中读取时，BOM 字节自动帮助检测当初写入流时采用的编码，以确保使用正确的解码器。对于从 Encoding 派生的一些类，这个方法返回 0 字节的数组——即没有前导码字节。显式构造 UTF8Encoding 对象，这个方法将返回一个 3 字节数组（包含 0xEF、0xBB 和 0xBF）。显式构造 UnicodeEncoding 对象，这个方法将返回一个 2 字节数组（包含 0xFE 和 0xFF）来表示“高位优先”（big-endian）编码，或者返回一个 2 字节数组（包含 0xFF 和 0xFE）来表示“低位优先”（little-endian）编码。默认认为低位优先。 |
| Convert | 将字节数组从一种编码（来源编码）转换为另一种（目标编码）。在内部，这个静态方法调用来源编码对象的 GetChars 方法，并将结果传给目标编码对象的 GetBytes 方法。结果字节数组返回给调用者。 |
| Equals | 如果从 Encoding 派生的两个对象代表相同的代码页和前导码设置，就返回 true。 |
| GetHashCode | 返回当前 Encoding 实例的哈希码。 |

# 14.6.1　字符和字节流的编码和解码

假定现在要通过 System.Net.Sockets.NetworkStream 对象来读取一个 UTF-16 编码字符串。字节流通常以数据块(data chunk)的形式传输。换言之，可能是先从流中读取 5 个字节，再读取 7 个字节。UTF-16 的每个字符都由 2 个字节构成。所以，调用 Encoding 的 GetString 方法并传递第一个 5 字节数组，返回的字符串只包含 2 个字符。再次调用 GetString 并传递接着的 7 个字节，将返回只包含 3 个字符的字符串。显然，所有 code point¹ 都会存储错误的值！

之所以会造成数据损坏，是由于所有 Encoding 派生都不维护多个方法调用之间的状态。要编码或解码以数据块形式传输的字符/字节，必须进行一些额外的工作来维护方法调用之间的状态，从而防止丢失数据。

字节块解码首先要获取一个 Encoding 派生对象引用(参见上一节)，再调用其 GetDecoder 方法。方法返回对一个新构造对象的引用，该对象的类型从 System.Text.Decoder 类派生。

① code point 是一个抽象概念。可将每个字符都想像成一个抽象的 Unicode code point，可能需要使用多个字节来表示一个 code point。——译注