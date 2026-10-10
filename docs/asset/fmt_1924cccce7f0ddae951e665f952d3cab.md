
```go
func (f *Foo) MarshalBinary(meta *encoder.Metadata) ([]byte, error) {
    buf, err := asn1.Marshal(*f)
    if err != nil {
        return nil, err
    }
    return buf, nil
}

func (f *Foo) Unmarshal(buf []byte, meta *encoder.Metadata) error {
    data := Foo{}
    if err := asn1.Unmarshal(buf, &data); err != nil {
        return err
    }
    *f = data
    return nil
}
```

列表 6-4：为 ASN.1 编码实现 `BinaryMarshallable` 接口

在 SMB 规范中。

位于 `https://github.com/blackhat-go/bhg/blob/master/ch-6/smb/ntlmssp/ntlmssp.go` 的 `ntlmssp` 包包含了 `MarshalBinary()` 和 `UnmarshalBinary()` 函数的另一种实现。尽管它没有演示 ASN.1，但起始代码展示了如何通过必要的元数据来处理任意数据类型的编码。这些元数据——变长字节切片的长度和偏移量——与编码过程密切相关。这些元数据引导我们进入了你需要解决的下一个挑战。

## 理解元数据和引用字段

如果你稍微深入研究 SMB 规范，你会发现某些消息包含了引用同一消息中其他字段的字段。例如，这些字段（取自 `Negotiate` 响应消息）引用包含实际值的变长字节切片的偏移和长度：

- `SecurityBufferOffset` (2 字节)：从 SMB2头部开始到安全缓冲区的偏移（以字节为单位）。
- `SecurityBufferLength` (2 字节)：安全缓冲区长度（以字节为单位）。

这些字段本质上充当了元数据。在消息规范的后续部分，你会找到数据实际所在的变长字段：

- `Buffer` (变长)：根据 `SecurityBufferOffset` 和 `SecurityBufferLength` 指定的包含响应安全缓冲区的变长缓冲区。该缓冲区 SHOULD 包含一个由第 3.3.5.4 节指定的 GSS 协议产生的令牌。如果 `SecurityBufferLength` 为 0，则此字段为空，并将使用客户端发起的认证（使用客户端选择的认证协议），而不是服务器发起的 SPNEGO 认证，如 [MS-AUTHSOD] 第 2.1.2.2 节所述。

通常来说，这就是 SMB 规范一致处理变长数据的方式：固定位置的长度和偏移字段描述了数据本身的大小和位置。这不仅适用于响应消息或 `Negotiate` 消息，而且你通常会在单个消息中发现多个使用这种模式的字段。实际上，只要你有变长字段，就会发现这种模式。元数据显式地指示消息接收者如何定位和提取数据。

这很有用，但它使编码策略变得复杂，因为你需要维护结构体内部不同字段之间的关系。例如，你不能仅仅只是序列化整个消息，因为由于元数据字段（例如长度和偏移量）在数据本身序列化之前（或者在偏移量的情况下，在数据之前的所有字段序列化之后）是不可知的。

## 理解 SMB 实现

本小节的剩余部分将介绍我们设计的 SMB 实现中一些复杂的细节。使用该包时不需要理解这些信息。

我们尝试了多种方法来处理引用数据，最终确定了一个结合结构体字段标签和反射的解决方案。回想一下，反射是一种程序可以检查自身的技术，特别是检查其自己的数据类型等内容。

字段标签（Field tags）与反射某种联系，因为它们定义了关于结构体字段的任意元数据。你可能在之前的 XML、MSPACK、JSON 编码示例中遇到过它们。例如，列表 6-5 使用结构体标签来定义 JSON 字段名。

```go
type Foo struct {
  A int `json:"a"`
  B string `json:"b"`
}
```

列表 6-5：一个定义 JSON 字段标签的结构体

Go 的 `reflect` 包包含了我们用于检查数据类型和提取字段标签的函数。在那个时候，只需要解析标签并对其值进行有意义的操作即可。在列表 6-6 中，你可以看到在 SMB 包中定义的结构体。

```go
type NegotiateRes struct {
  Header
  StructureSize uint16
  SecurityMode uint16
  DialectRevision uint16
  Reserved uint16
  ServerGuid []byte `smb:"fixed:16"`
  Capabilities uint32
  MaxTransSize uint32
  MaxReadSize uint32
  MaxSize uint32
  SystemTime uint64
  ServerStartTime uint64
  SecurityBufferOffset uint16 `smb:"offset:SecurityBlob"`
  SecurityBufferLength uint16 `smb:"len:SecurityBlob"`
  Reserved2 uint32
  SecurityBlob *gss.NegTokenInit
}
```

列表 6-6：使用 SMB 标签定义字段元数据 (/ch-6/smb/smb.go)

该类型使用了三个字段标签，通过 SMB 键识别：`fixed` ①、`offset` ② 和 `len` ③。请记住，我们选择这些名称都是随机的。你没有义务使用特定的名称。每个标签的意图如下：

- `fixed` 将 `[]byte` 识别为指定大小的固定长度字段。在这种情况下，`ServerGuid` 的长度为 6 字节。
- `offset` 定义了从结构体开始到变长数据缓冲区第一部分的字节数。该标签定义了字段名称——在此例中为 `SecurityBlob`——偏移量与之相关。预期同一结构体中存在一个该引用引名的字段。
- `len` 定义了变长数据缓冲区的长度。该标签定义了字段名称——在此例中为 `SecurityBlob`——`len` 与之相关。同一结构体中应该存在一个该引用引名的字段。

正如你可能注意到的，我们的标签不仅允许我们通过任意元数据在不同字段之间建立关系，还允许区分固定长度字节和变长数据。

## 解析和存储标签

在列表 6-7 中，便利函数 `parseTags()` 执行标签解析并将数据存储在名为 `TagMap` 的自定义 map 中。

```go
func parseTags(sf reflect.StructField) (*TagMap, error) {
	ret := &TagMap{
		m: make(map[string]interface{}),
		has: make(map[string]bool),
	}
	tag := sf.Tag.Get("smb")
	if tag == "" {
		return ret, nil
	}
	smbTags := strings.Split(tag, ",")
	for _, smbTag := range smbTags {
		tokens := strings.Split(smbTag, ":")
		switch tokens[0] {
		case "len", "offset", "count":
			if len(tokens) != 2 {
				return nil, errors.New("missing required tag. Expecting key:val")
			}
			ret.m[tokens[0]] = tokens[1]
			ret.has[tokens[0]] = true
		case "fixed":
			if len(tokens) != 2 {
				return nil, errors.New("missing required tag. Expecting key:val")
			}
			i, err := strconv.Atoi(tokens[1])
			if err != nil {
				return nil, err
			}
			ret.m[tokens[0]] = i
		}
	}
	return ret, nil
}
```

列表 6-7：解析结构标签 (/ch-6/smb/encoder/encoder.go)

## 调用 parseTags() 函数和创建 reflect.StructField 对象

现在，我们如何调用该函数以及如何创建 `reflect.StructField` 对象？为了回答这些问题，请查看列表 6-8 中的 `unmarshal()` 函数，它位于包含 `parseTags()` 便利函数的同一个源文件中。`unmarshal()` 函数非常长，所以我们只拼接最相关的部分。

```go
func unmarshal(buf []byte, v interface{}, meta *Metadata)(interface{}, error) {
	typev := reflect.TypeOf(v)
	value := reflect.Value(v)
	// ... code ...
	r := bytes.NewBuffer(buf)
	switch typev.Kind() {
	case reflect.Struct:
		// ... code ...
	case reflect.Uint8:
		// ... code ...
	case reflect.Uint16:
		// ... code ...
	case reflect.Uint32:
		// ... code ...
	case reflect.Uint64:
		// ... code ...
	case reflect.Slice, reflect.Array:
		// ... code ...
	default:
		// ... code ...
	}
	return errors.New("Unmarshal not implemented for kind:" + 
	typev.Kind.String()), nil
}
return nil, nil
}
```

列表 6-8: 使用反射动态反序列化未知类型 (/ch-6/smb/encoder/encoder.go)

`Unmarshal()` 函数使用 Go 的 `reflect` 包来获取目标接口的类型和值，我们的数据缓冲区将被反序列化到该接口中。这是必要的，因为为了将任意字节切片转换为结构体，必须知道结构体中有多少个字段，以及每个字段需要读取多少字节数据。例如，定义为 `uint16` 的字段消耗 2 个字节，而 `uint64` 则消耗 8 个字节。通过反射，我们查询目标接口以查看它是一个什么类型的数据类型，以及如何处理数据的读取。由于每种类型的逻辑都不同，我们通过调用 `type.Kind()` 对类型进行 `switch` 分判断，该方法返回一个 `reflect.Kind` 实例，指示我们正在处理的数据类型种类。你会发现我们为每个允许的数据类型都编写了单独的 `case`。

## 处理结构体

让我们看看列表 6-9 中的 `case` 块，它处理结构体类型，因为这很可能是初始的入口点。

```go
case reflect.Struct:
    m := &Metadata{
    Tags: &TagMap{},
    Lens: make(map[string]uint64),
    Parent: v,
    ParentBuf: buf,
    Offsets: make(map[string]uint64),
    CurrOffset: 0,
    }
    for i := 0; i < typev.NumField(); i++ {
        m.CurrField = typev.Field(i).Name
        tags, err := parseTags(typev.Field(i))
        if err != nil {
            return nil, err
        }
        m.Tags = tags
        var data interface{}
        switch typev.Field(i).Kind() {
        case reflect.Struct:
            data, err = unmarshal(buf[m.CurrOffset:],
            typev.Field(i).Interface(), m)
        default:
            data, err = unmarshal(buf[m.CurrOffset:],
            typev.Field(i).Interface(),)
        }
        if err != nil {
            return nil, err
        }
        typev.Field(i).Indirect().Set(ValueOf(data))
        v = reflect.Indirect(ValueOf(v)).Interface()
        meta.CurrOffset += m.CurrOffset
        return v, nil
    }
}
```

列表 6-9: 反序列化结构体类型 ((ch-6/smb/smb/encoder/encoder.go))

`case` 块开始定义了一个新的 `Metadata` 对象，该类型用于跟踪相关的元数据，包括当前缓冲区偏移量、字段标签和其他信息。使用我们的类型变量 `typev`，我们调用 `NumField()` 方法来获取结构体中的字段数量。它返回一个整数值，作为循环的约束条件。

在循环内部，我们可以通过调用类型的 `Field(index int)` 方法来提取当前字段。该方法返回 `reflect.StructField` 类型。你会发现我们在整个代码段中多次使用了该方法。可以将其想为通过索引值从切片中获取元素。我们的第一次使用是获取字段以提取其名称。例如，`SecurityBufferOffset` 和 `SecurityBlob` 是列表 6-6 中定义的 `NegotiRes` 结构体内的字段名。字段名被赋值给 `Metadata` 对象的 `CurField` 属性。第二次调用 `Field(index int)` 方法输入到列表 6-7 的 `parseTags()` 函数中。我们知道这个函数解析我们的结构体字段标签。标签被包含在我们的 `Metadata` 对象中，以便稍后跟踪和使用。

接下来，我们使用 `switch` 语句专门对字段类型进行操作。只有两种情况。第一种处理字段本身是结构体的情况，在这种情况下，我们对 `Unmarshal()` 函数进行递归调用，并将字段指针作为接口传递给它。第二种情况处理所有其他类型（基本类型、切片等），递归地调用 `Unmarshal()` 函数并将字段本身作为接口传递。这两种情况都进行了一些“特殊操作”，以使缓冲区从我们的当前偏移量开始移动。我们的递归调用最终返回一个 `interface()`，这是一个包含我们反序列化后的数据的类型。我们使用反射将当前字段的值设置为该接口数据。最后，我们会在缓冲区中推进当前的偏移量。

哎呀！你能看到这在开发上可能是多大的挑战吗？我们为每种输入都准备了单独的 `case`。幸运的是，处理结构体的 `case` 是最复杂的。

## 处理 uint16

如果你非常关注，你可能会问：你到底从缓冲哪里读取数据？答案是列表 6-9 中哪里都没有。回想一下，我们对 `Unmarshal()` 函数进行递归调用，每次我们都将内部字段传递给该函数。最终我们将到达基本数据类型。毕竟，在某一点，最内层的嵌套结构是由基本数据类型组成的。当我们遇到基本类型时，我们的代码将匹配最外层 `switch` 语句中的不同 `case`。例如，当我们遇到 `uint16` 数据类型时，这段代码将执行列表 6-10 中的 `case` 块。

```go
case reflect.Uint16:
    var ret uint16
    if err := binary.Read(r, binary.LittleEndian, &ret); err != nil {
        return nil, err
    }
    if meta.Tags.Has("len") {
        err := meta.Tags.GetInt("len")
        if err != nil {
            return nil, err
        }
        meta.Lens[meta.CurrField] = uint64(ret)
    }
    meta.CurrOffset += uint64(binary.Size(ret))
    return nil, err
}
```

列表 6-10: 反序列化 uint16 (ch-6/smb/encoder.go)

在这种情况下，我们调用 `binary.Read` 从缓冲区读取数据到一个变量。回想一下，我们对 `Unmarshal()` 函数进行递归调用，每次我们都将内部字段传递给该函数。最终我们将到达基本数据类型。毕竟，在某一点，最内层的嵌套结构是由基本数据类型组成的。当我们遇到基本类型时，我们的代码将匹配最外层 `switch` 语句中的不同 `case`。例如，当我们遇到 `uint16` 数据类型时，这段代码将执行列表 6-10 中的 `case` 块。接下来，我们检查 `len` 标签是否存在。如果存在，我们获取该值——即与该偏移量相关的数值。因为字段实际上位于 SMB 消息中，我们知道了需要读取多少字节。我们根据数据的大小推进当前偏移量。我们刚刚获取了元数据，将其存储在 `Metadata` 中维护字段名与长度关系的映射表中。

## 处理切片

在列表 6-11 中，你可以看到处理切片的 `case` 块，我们需要利用标签和元数据处理固定长度和变长的数据。
