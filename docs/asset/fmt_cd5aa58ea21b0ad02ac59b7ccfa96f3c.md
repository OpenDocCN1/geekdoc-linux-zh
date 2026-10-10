
```javascript
function CaesarEncrypt(key, plaintext)
{
  var result = "";
  var key = parseInt(key);
  plaintext = plaintext.toUpperCase();

  var length = plaintext.length;
  for (var i = 0; i < length; i++) {
    var val = plaintext.charCodeAt(i) - 65;
    if (val >= 0) {
      result += String.fromCharCode((val + key) % 26) + 65);
    }
  }
  return result;
}

function HandleEncrypt()
{
  var key;
  var plaintext;

  // To done: get the key
  key = document.getElementById("key").value;

  // To done: get the plaintext
  plaintext = document.getElementById("plaintext").value;

  // compute the ciphertext
  var ciphertext = CaesarEncrypt(key, plaintext);

  // To done: set the value of the text field to ciphertext
  document.getElementById("ciphertext").value = ciphertext;
}
```

# Trixul

现在我们已经有了这些函数，让我们尝试完成前面代码中的“To done”项目。我们先查看描述窗口的标记：

```xml
<window name="main" title="Caesar" main="true"
width="320" height="200" x="100" y="100">

  <!--UI to obtain the plaintext message to -->
  <box orient="horizontal">
    <statictext string="Plaintext:" width="130"/>
    <text editable="true" selectable="true" id="plaintext" string="Enter message" width="300"/>
  </box>

  <!--UI to get the key value from the user -->
  <box orient="horizontal">
    <statictext string="Key:" width="130"/>
    <text editable="true" selectable="true" id="key" string="1" width="50"/>
  </box>

  <!--UI to display the resulting ciphertext -->
  <box orient="horizontal">
    <statictext string="Ciphertext:" width="130"/>
    <statictext id="ciphertext" string="" width="100"/>
  </box>

  <spacer/>

  <!--button box -->
  <box orient="horizontal">
    <spacer/>
  </box>
</window>
```

```xml
<button onclick="HandleEncrypt();"
  label="Encrypt"/>
  <spacer>
  <button onclick="quit();" label="Quit"/>
  <spacer>
</button>
```

| Plaintext | Hello World |
|---|---|
| Key | 3 |
| Ciphertext | KHOOR ZRUOG |

Figure 9-17 Caesar Cipher GUI

# Trixul 493

```javascript
var ciphertext = CaesarEncrypt(key, plaintext);

// display the result

document.getElementById("ciphertext").value =
ciphertext;
```

上述使用 `getElementById` 获取对象，并随后读取和写入其 `value` 属性的操作，是一种在 DHTML 代码和 XUL 应用中被广泛使用的模式。

观察此功能在底层是如何实现的很有启发意义——通过观察 Trixul 和嵌入式 JavaScript 引擎如何处理以下表达式：

`key = document.getElementById("key");`

可以学习到很多关于 JavaScript 如何与 Trixul DOM 集成的知识。要理解它的工作原理，需要先理解 DOM 对象和 JavaScript 对象是如何相互相关的。

## 将 DOM 文档和元素对象映射到 JavaScript 对象

故事始于文档 XML 源码的解析。记住，DOM 是解析产生的结果，用于表示文档，XML 文档中的每个元素都由 DOM 层次结构数据结构中的一个节点表示。从元素解析出的属性会与元素一起存储在 DOM 中；这包括元素的 `id` 属性（如果在标记中指定了该属性）。给定的 `id`，Trixul 可以搜索 DOM 以找到对应的元素。

在 DOM 中的元素处理完毕后，布局引擎会获取一个单例 Trixul 对象的实例，该对象提供了与嵌入式 SpiderMonkey JavaScript 引擎交互的 C++ 接口。它调用该对象定义的函数来创建一个表示 DOM 文档的 JavaScript 对象。该 JavaScript 文档对象就可以被与同一文档相关的任何用户编写的 JavaScript 代码引用，如代码所示，它使用 `document` 对象来调用 `getElementById()`。重要的是，SpiderMonkey 引擎返回的 JavaScript 对象存储在一个映射中，该映射包含一个指向其所代表的 DOM 文档对象的指针。我们把这个映射称为 `DocumentMap`。

# 494 第 9 章 使用 C++ 开发跨平台 GUI 工具包

在描述如何使用 `DocumentMap` 之前，让我们关注 `getElementById(id)` 函数的实现。SpiderMonkey JavaScript 引擎允许 Trixul 在创建 JavaScript 对象时，定义诸如 `getElementById(id)` 的函数，这些函数可以从用户脚本在这些对象上被调用。Trixul 还可以创建属性，这些属性可以像 C 语言中的字段一样被引用。`getElementById(id).value` 中的 `.value` 部分就是代码如何访问对象上定义的值属性的示例。下面，我将描述值引用的实现方式，但让我们继续对 `getElementById(id)` 函数的讨论。

对象可以定义的函数数量或其名称没有限制。然而，这些函数必须由嵌入 SpiderMonkey JavaScript 引擎的代码映射到 C 函数。当 JavaScript 对象创建时，SpiderMonkey 引擎会获取一个 C 结构体数组，该数组将函数名（例如 `getElementById(id)`）映射到 Trixul 布局引擎实现的相应 C 函数。例如，JavaScript 函数 `getElementById()` 必须映射到名为 `HandGetElementById()` 的 Trixul 函数。（在接后的文中我将假设存在这样的映射。）

假设我们已经在 JavaScript 引擎中创建了一个对象，并且如上所述已在该对象上定义了 `getElementById()` 函数。当用户调用 `document.getElementById("key")` 时，SpiderMonkey JavaScript 引擎将调用 `HandGetElementById()` 并向其传递两个参数：1) 调用该函数的 JavaScript DOM 对象的副本， 2) 调用者传递给 `getElementById()` 的 `id` (`key`)。拿到这个 JavaScript 对象后，Trixul 可以轻松地在 `DocumentMap` 中查找对应的 DOM 对象。从映射中检索 DOM 对象后，Trixul 可以搜索 DOM 以寻找包含指定 `ID` 的元素。如果找到了元素，我们就会调用 SpiderMonkey 函数创建另一个 JavaScript 对象，这次用于表示我们找到的 DOM 元素（见图 9-18）。
