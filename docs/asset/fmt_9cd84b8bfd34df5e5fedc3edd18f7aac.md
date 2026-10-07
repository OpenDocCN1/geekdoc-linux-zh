
# 第 9 章 使用 C++ 一个跨平台 GUI 工具包

## Trixul

上述代码执行的步骤包括：

- 1. 获取基于 `NSPR` 的库对象，并利用它解析指向 C++ 创建者和析构函数的指针。
- 2. 创建基础 JavaScript 对象。
- 3. 调用库的创建者函数，该函数将实例化 C++ 类。将基础 JavaScript 对象作为参数传递，以便 C++ 对象可以存储对它的引用。
- 4. 对于为类定义的每个函数，解析指向库中定义的 C++ 代理函数的引用，然后在 JavaScript 对象上定义一个函数，该函数在被调用时将调用代理函数。

让我们逐一通过这些步骤。

### 解析库中创建者函数和析构者函数的指针

`ComponentManager` 对象（其引用存储在 `Object` 中）包含一个指向 `NSPR` 库对象的指针。使用该库，我们必须解析出两个函数的指针。第一个是创建者函数 `Creator`，用于创建类的实例。第二个是析构者函数 `Destroyer`，用于删除这些实例。每个 C++ 组件库必须将这些函数作为导出函数提供。创建者和析构函数的名称分别为 `NewClassProxy()` 和 `DeleteClassProxy()`，其中 `Class` 是类名。

### 创建基础 JavaScript 对象

SpiderMonkey JavaScript 引擎通过 `JS_DefineObject()` 函数支持创建 JavaScript 对象。详细描述 SpiderMonkey 引擎不在本书的讨论范围内，但我确实想通俗地详细介绍如何执行对象创建。这将有助于澄清 JavaScript 对象与从组件库实例化的 C++ 对象之间的桥接。

在调用 `JS_DefineObject` 之前，必须分配并初始化一个 `JSClass` 结构体。在这里，我简单地提供了类名，并对结构体中的其余字段使用默认 stub 值：

```cpp
JSClass objectClass = {
  m_name.c_str(), 0,
  JS_PropertyStub, JS_PropertyStub,
  JS_PropertyStub, JS_PropertyStub,
  JS_EnumerateStub, JS_ResolveStub,
  JS_ConvertStub, JS_FinalizeStub
};
```

`m_jsClass = objectClass;`

接下来，我调用 `JS_DefineObject()` 来创建 JavaScript 对象。一旦创建，对象的指针将被存储为成员函数。从 JavaScript 调用 `ComponentManager` 的 `getObject()` 方法，将返回此对象：

```cpp
m_jsObj = JS_DefineObject(ctx, obj, name.c_str(),
    &m_jsClass, NULL, 0);
```

### 实例化 C++ 对象

现在我们有了 JavaScript 对象，通过调用共享库中上述创建者函数来创建 C++ 类实例。创建者函数将实例化类并将其添加到静态映射中，以 JavaScript 对象作为索引。稍后，我们可以使用 JavaScript 对象作为索引轻松地查找 C++ 对象。

### 在基础 JavaScript 对象上定义 JavaScript 函数

每个 JavaScript 函数通过其名称定义，当 JavaScript 程序调用该函数时，将调用共享库中 C++ 代理函数的地址。正如你稍后看到的，由 Trixul 生成的代理函数是在运行时将 JavaScript 对象绑定到 C++ 对象的魔术。对于 SIL 文件中为类定义的每个函数，Trixul 会生成相应语言函数的源码。对于那些熟悉 Java 原生接口 `JNI` 的人来说，Trixul 的做法在某种程度上是类似的，区别在于 Trixul 不仅生成头文件，还生成了实现。这些代理函数必须链接到包含相应类实现的共享库。代理函数具有 JavaScript 引擎强制要求的预定义签名。这里是 `Encrypt` 的代理函数：

```cpp
JSBool
Encrypt(JSContext *cx, JSObject *obj, unsigned argc, jsval *);
```

`Encrypt()` 是一个由 Trixul 生成的函数，它使用 JavaScript 对象作为索引从映射中查找 C++ 实例，然后调用其成员函数。在调用 `Encrypt()` 之前，传入的 JavaScript 参数转换为 C++ 类型。在调用 `Encrypt()` 后，返回值从 C++ 类型转换为 JavaScript 类型。

## 从 SIL 文件生成代理源码和 C++ 类

正如上一节所示，位于 JavaScript 对象和组件库实例之间的代理代码由 Trixul 生成并必须链接到组件库。在本节中，我将描述生成的代理代码并讨论 C++ 组件是如何定义的。

给定一个 SIL 文件，可以通过命令行调用 Trixul 来生成代理代码的源码和头文件，以及包含每个类定义的头文件。以下是 Trixul 执行这些任务时接受的参数：

- `p` 要处理的 SIL 文件路径
- `h` Trixul 生成的代理头文件路径
- `s` Trixul 生成的代理源码路径
- `c` 定义 SIL 文件中类的源码路径

以下命令行调用 Trixul 处理 SIL 文件 `components/encrypt.sil` 并在指定位置生成相应的代理头和源码：

```bash
trixul -p components/encrypt.sil -h components/encrypt_proxy.h \
-s components/encrypt_proxy.cpp -c encrypt.h
```

以下列表了上述命令行生成的代码。首先是头文件 `encrypt.h`，声明了由 JavaScript 引擎调用的 C 语言函数原型：

```cpp
// 这是生成的源码。请勿编辑 //
#if defined(__79463AD7_02C3_42FD__)
#define __79463AD7_02C3_42FD__ A8F0_061525CA5FF8_PROXY_H__
#endif
```

```cpp
#include <prtypes.h>
#include "jsapi.h"
extern "C" EXPORT JSBool
Encrypt_Get_key(JSContext *cx, JSObject *obj,
unsigned argc, jsval *argv, jsval *rval);
extern "C" EXPORT JSBool
Encrypt_Set_key(JSContext *cx, JSObject *obj,
unsigned argc, jsval *argv, jsval *rval);
extern "C" EXPORT JSBool
Encrypt_Set_key(JSContext *cx, JSObject *obj,
unsigned argc, jsval *argv, jsval *rval);
```

### Trixul 511

```cpp
extern "C" EXPORT JSBool
AESEncrypt(JSContext *cx, JSObject *obj,
uint argc, jval *argv, jval *rval);
```

```cpp
extern "C" EXPORT JSBool
AESDecrypt(JSContext *cx, JSObject *obj,
uint argc, jval *argv, jval *rval);
```

```cpp
extern "C" EXPORT PRStatus
NewAESEncryptProxy(JSObject *obj);
```

```cpp
extern "C" EXPORT PRStatus
DeleteAESEncryptProxy(JSObject *obj);
```

下一个列表是头文件 `components/encrypt.h`，它包含了名为 `AESEncrypt` 的 C++ 类的声明。`Get_key()` 和 `Set_key()` 是支持 `AESEncrypt` 密钥属性的公共函数。在 Trixul 中，属性作用域于对象，并实现为相应类中的成员变量。剩余的函数 `SetKey()`、`Encrypt()` 和 `Decrypt()` 对应于 SIL 中该类的接口：

```cpp
// 这是生成的源代码。请勿编辑 //
#if defined(__79463AD7_02C3_42FD_A8F0_)
#define 061S2C4S5F8_COMP_H___
#define __79463AD7_02C3_42FD_A8F0_
#define 061S2C4S5F8_COMP_H__
#include "types.h"
#include <string>
using namespace std;
class AESEncrypt {
public:
  AESEncrypt();
  ~AESEncrypt();
  PRStatus Get_key(string& val) {val = m_key; return PR_SUCCESS;}
  PRStatus Set_key(string& val) {m_key = val; return PR_SUCCESS;}
  PRStatus SetKey(string&);
  string Encrypt(string& Plaintext);
  string Decrypt(string& Ciphertext);
private:
string m_key;
};
#endif
```

最后，后续文件 `components/encrypt_proxy.cpp` 实现了用于将 JavaScript 对象与 `AESEncrypt()` 类实例连接起来的 STL `map`，以及在代理源码中支持添加、删除和查找 C++ 类的函数（分别为 `AddAESEncryptClass()`、`RemoveAESEncryptClass()` 和 `GetAESEncryptClass()`）。此外，创建和销析器函数（分别为 `NewAESEncryptProxy()` 和 `DeleteAESEncryptProxy()`）以及代理函数的源代码也定义在 Trix 生成的源文件中：

```cpp
// 这是生成的代码。请勿编辑 /*
#include "encrypt_proxy.h"
#include "encrypt.h"
#include "prtypes.h"
#include "jsstr.h"
#include <map>
using namespace std;
static map<JSONObject *, AESEncrypt*> objAESEncryptMap;
static AESEncrypt *
GetAESEncryptClass(JSONObject *obj)
{
    return objAESEncryptMap[obj];
}
static void
AddAESEncryptClass(JSONObject *obj, AESEncrypt *cPtr)
{
    objAESEncryptMap[obj] = cPtr;
}
static void
RemoveAESEncryptClass(JSONObject *obj)
{
    objAESEncryptMap.erase(obj);
}
extern "C" EXPORT PRStatus
NewAESEncryptProxy(JSObject *obj)
{
    AESEncrypt *ptr = new AESEncrypt();
    if (!ptr)
        return PR_FAILURE;
    AddAESEncryptClass(obj, ptr);
    return PR_SUCCESS;
}
```

```cpp
extern "C" EXPORT PRStatus
DeleteAESEncryptProxy(JSObject *obj)
{
    AESEncrypt *ptr;
    if (obj) {
        ptr = GetAESEncryptClass(obj);
        RemoveAESEncryptClass(obj);
    }
    return PR_SUCCESS;
}
```

```cpp
extern "C" EXPORT JSBool
AESEncrypt_SetKey(JSContext *cx, JSObject *obj,
unsigned int argc, JSValue *argv, JSValue *rval)
{
    AESEncrypt *ptr = GetAESEncryptClass(obj);
    if (!ptr)
        return JS_FALSE;
    JSString *str_0 = JSVAL_TO_STRING(argv[0]);
    string arg_0(JS_GetCStringBytes(str_0));
    ptr->SetKey(arg_0);
    return JS_TRUE;
}
```

```cpp
extern "C" EXPORT JSBool
AESEncrypt_Encrypt(JSContext *cx, JSObject *obj,
unsigned int argc, JSValue *argv, JSValue *rval)
{
    AESEncrypt *ptr = GetAESEncryptClass(obj);
    if (!ptr)
        return JS_FALSE;
    JSString *str_0 = JSVAL_TO_STRING(argv[0]);
    string arg_0(JS_GetCStringBytes(str_0));
    string ret;
    ret = ptr->Encrypt(arg_0);
    JSString *str = ::JS_NewStringCopy(cx,
    ret.c_str(), ret.size() + 1);
    rval = STRING_TO_JSVAL(str);
    return JS_TRUE;
}
```

```cpp
extern "C" EXPORT JSBool
AESEncrypt_Decrypt(JSContext *cx, JSObject *obj,
unsigned int argc, JSValue *argv, JSValue *rval)
{
    AESEncrypt *ptr = GetAESEncryptClass(obj);
    if (!ptr)
        return JS_FALSE;
    JSString *str_0 = JSVAL_TO_STRING(argv[0]);
    string arg_0(JS_GetCStringBytes(str_0));
    string ret;
    ret = ptr->Decrypt(arg_0);
    JSString *str = ::JS_NewStringCopy(cx,
    ret.c_str(), ret.size() + 1);
    rval = STRING_TO_JSVAL(str);
    return JS_TRUE;
}
```

## 编写实现组件的 C++ 代码

剩余的是实现该组件的 C++ 代码。这些代码由组件开发者提供，而不是由 Trixul 生成。Trixul 本来可以为类定义的每个函数生成存根 `stub`，但我设计的决定是限制 Trixul 只生成类的头文件，并将实现留给组件开发者。以下是我编写的实现 `AESEncrypt()` 的代码，你可以看到它包含了 Trixul 生成的 `encrypt.h` 以及 `gcrypt.h`，后者使用了 GNU 库 `libgcrypt` 通过 AES 算法执行加密：

```cpp
#include "encrypt.h"
#include <gcrypt.h>
AESEncrypt::AESEncrypt()
{
}
AESEncrypt::~AESEncrypt()
{
}
PRStatus
AESEncrypt::SetKey(string& Key)
{
    m_key = Key;
    return PR_SUCCESS;
}
string AESEncrypt::Encrypt(string& Plaintext)
{
  gcry_cipher_hd_t hd = 0;
  gcrypt_error_t err = 0;
  char *iv = "1234567812345678";
  char ctext[128] = "";
  char actext[256] = "";
  err = gcry_cipher_open(&hd, GCRY_CIPHER_AES,
  GCRY_CIPHER_MODE_CFB, 0);
  if (err) {
    err = gcry_cipher_setkey(hd, m_key.c_str(),
    m_key.length());
  }
  if (err) {
    err = gcry_cipher_setiv(hd, iv, strlen(iv));
  }
  if (err) {
    err = gcry_cipher_encrypt(hd, ctext,
    sizeof(ctext), Plaintext.c_str(),
    Plaintext.length());
  }
```
