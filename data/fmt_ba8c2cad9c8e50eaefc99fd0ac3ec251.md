
值得注意的是，Go 动态地序列化登录响应，只填充呈现的字段，这意味着我们可以使用单个结构体格式表示成功和失败的登录。

## 创建配置结构体和 RPC 方法

在列表 3-15 中，你采用了定义的类型并实际使用它们，创建向 `Metasploit` 发出 `RPC` 命令的必要方法。与 `Shodan` 示例一样，你定义了一个任意类型来维护相关的配置和身份验证信息。这样，你就不需要显式且重复地传递主机、端口和身份标记等公共元素。相反，你将使用该类型并在其上构建方法，以便数据隐式可用。

```go
type Metasploit struct {
	host string
	user string
	pass string
	token string
}
```

```go
func New(host, user, pass string) *Metasploit {
	msf :=&Metasploit{
		host: host,
		user: user,
		pass: pass,
	}
	return msf
}
```

列表 3-15：定义 (`/ch-3/metasploit-minimal/rpc/msf.go`)

## 执行远程调用

现在你有一个结构体，并且为了方便起见，有一个名为 `New()` 的函数可以初始化一个新的结构体。你现在可以在 `Metasploit` 类型上构建方法以执行远程调用。为了防止代码重复，在列表 3-16 中，你通过构建一个处理序列化、反序列化的方法开始。`send()` 方法接收请求和响应参数，类型为 `interface{}`。使用此接口允许将任何结构体传递给方法，随后将请求发送服务器。接下来，使用 `msgpack` 库编码请求：通过 `NewEncoder()` 创建编码器然后调用 `Encode()` 方法。这为 `buf` 变量填充 `MessagePack` 编码的请求表示。编码完成后，使用数据构建目标 `URL` 并发出 `POST` 请求，内容类型设置为 `binary/message-pack` 并设置请求体。最后，你解码响应体。正如之前提到的，解码后的数据被写入传入方法的内存位置。数据的编码和解码无需显式知道请求或响应结构体类型，使得该方法灵活且可复用。

```go
func (msf *Metasploit) send(req interface{}, res interface{}) error {
	buf := new(bytes.Buffer)
	msgpack.NewEncoder(buf).Encode(req)
	dest := fmt.Sprintf("http://%s/api", msf.host)
	r, err := http.Post(dest, "binary/message-pack", buf)
	if err != nil {
		return err
	}
	defer r.Body.Close()
	if err := msgpack.NewDecoder(r.Body).Decode(res); err != nil {
		return err
	}
	return nil
}
```

列表 3-16：带有序列化和反序列化的通用 `send()` 方法 (`/ch-3/metasploit-minimal/rpc/msf.go`)

在列表 3-17 中，你可以看到逻辑的核心部分。

```go
func (msf *Metasploit) Login(①) error {
	ctx := &loginReq{
		Method: "auth.login",
		Username: msf.user,
		Password: msf.pass,
	}
	var loginRes
	if err := msf.send(ctx, &res)②; err != nil {
		return err
	}
	msf.token = loginRes.Token
	return nil
}

func (msf *Metasploit) Logout(③) error {
	ctx := &logoutReq{
		Method: "auth.logout",
		Token: msf.token,
		btnLogout: msf.token,
	}
	var logoutRes
	if err := msf.send(ctx, &res)④; err != nil {
		return err
	}
	msf.token = ""
	return nil
}
```

```go
func (msf *Metasploit) SessionList() (map[uint32]SessionList, error) {
	req := &SessionListReq{Method: "session.list", Token: msf.token}
	res := make(map[uint32]SessionList)
	if err := msf.send(req, &res); err != nil {
		return nil, err
	}

	for id, session := range res {
		session.ID = id
		res[id] = session
	}
	return res, nil
}
```

列表 3-17: `Metasploit` `API` 调用实现 (`/ch-3/metasploit-minimal/rpc/ms.go`)

你定义了三个方法：`Login()` ①、`Logout()` ③ 和 `SessionList()` ⑤。每个方法都使用相同的通用流程：创建并初始化一个请求结构体，创建响应结构体，并调用辅助函数 ④ ⑦ 来发送请求并接收解码后的响应。`Login` 和 `Logout` 方法操作的是 `token` 属性。方法逻辑之间唯一的显著差异出现在 `SessionList()` 方法中，在该方法中，你将响应定义为 `map[uint32]SessionList` ⑥，并遍历该响应以展平 map ⑧，在结构体上设置 `ID` 属性，而不是维护一个 map map。

记住，`session.list()` 函数需要一个有效的身份验证令牌，这意味着在调用 `SessionList()` 方法成功之前，你必须登录。列表 3-18 使用 `Metasploit` 接收器结构体来访问 `token`，该值并不是有效值——它是一个空字符串。由于你在这里开发的程序并不完整，你可以直接在 `SessionList()` 方法内部显式包含一个对 `Login()` 方法的调用，但对于每实现一个额外的身份验证方法，你都必须检查有效身份验证令牌的存在并显式地调用 `Login()`。这并不是良好的编码实践，因为你将花费大量时间重复逻辑，而这些逻辑你可以写在引导过程的一部分中。

你已经实现了一个函数 `New()`，它被设计用于引导，因此请修补该函数，看看将身份验证作为过程的一部分时，新的实现看起来是什么样的（参见列表 3-18）。

```go
func New(host, user, pass string) (*Metasploit, error) {
	msf := &Metasploit{
		host: host,
		user: user,
		pass: pass,
	}

	if err := msf.Login(); err != nil {
		return nil, err
	}

	return msf, nil
}
```

列表 3-18: 通过嵌入 `Metasploit` 登录初始化客户端 (`/ch-3/metasploit-minimal/rpc/msf.go`)

修补后的代码现在将错误作为返回值集合的一部分。这是为了警报可能的身份验证失败。此外，逻辑中还增加了对 `Login()` 方法的显式调用。只要使用此 `New()` 函数实例化 `Metasploit` 结构体，你的身份验证方法调用现在就可以访问有效的身份验证令牌了。

## 创建实用工具程序

在本示例的末尾，你的最后一项工作是创建一个实现你那闪亮新库的实用工具程序。将列表 3-19 中的代码输入 `client/main.go`，运行它，并见证奇迹发生。

```go
package main

import (
	"fmt"
	"log"

	"github.com/blackhat-go/bhg/ch-3/metasploit-minimal/rpc"
)

func main() {
	host := os.Getenv("MSHOST")
	pass := os.Getenv("MSFPASS")
	user := "msf"

	if host == "" || pass == "" {
		log.Fatal("缺少必需的环境变量 MSHOST 或 MSFPASS")
	}
	msf, err := rpc.New(host, user, pass)
	if err != nil {
		log.Panicln(err)
	}
	defer msf.Logout()

	sessions, err := msf.SessionList()
	if err != nil {
		log.Panicln(err)
	}
	fmt.Println("Sessions:")
	for _, session := range sessions {
		fmt.Printf("%5d %s\n", session.ID, session.Info)
	}
}
```

列表 3-19: 使用我们的 `msfrpc` 包 (`/ch-3/metasploit-minimal/client/main.go`)

首先，引导 `RPC` 客户端并初始化一个新的 `Metasploit` 结构体。记住，你刚刚更新了该函数以在初始化期间执行身份验证。接下来，通过通过延迟调用 `Logout()` 方法来确保进行清理工作。这将在 `main` 函数返回或退出时运行。然后你调用 `SessionList()` 方法并遍历响应以列出可用的 `Meterpreter` 会话。

代码虽然很多，但幸运的是，实现其他 `API` 调用的工作应该少得多，因为你只需要定义请求和响应类型，并构建发布远程调用的库方法。以下是直接从我们的客户端工具程序产生的示例输出，显示了一个已建立的 `Meterpreter` 会话：

```
$ go run main.go
Sessions:
 WIN-HOME\smith @ WIN-HOME
```

这样。你成功地创建了一个库和一个客户端工具程序，用于与远程 `Metasploit` 实例交互以检索可用的 `Meterpreter` 会话。接下来，你进入元数据领域。

## 通过爬取解析元数据

正如我们在本章中强调的，`ZIP` 文件在解压时包含元数据。`core.xml` 文件也包含这些信息。它的结构如下：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<cp:coreProperties
xmlns:cp="http://schemas.openxmlformats.org/package/2006/metadata"
  xmlns:dc="http://www.purl.org/dc/elements/1.1/"
  xmlns:dcterms="http://www.purl.org/dc/terms"
  xmlns:dccmity="http://www.purl.org/dc/dccmity"
  xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <dc:creator>Dan Kottmann</dc:creator>
  <cp:lastModifiedBy>Dan Kottmann</cp:lastModifiedBy>
  <dcterms:created></dcterms:created>
  <dcterms:modified xsi:type="dcterms:W3TF">2016-12-06T18:24:42Z</dcterms:modified>
  <dcterms:modified xsi:type="dcterms:W3TF">2016-12-06T18:25:32Z</dcterms:modified>
</cp:coreProperties>
```

`creator` 和 `lastModifiedBy` 元素是主要关注点。这些字段包含了你可以用于社会工程或密码破解攻击的员工姓名或用户名。

```xml
<lspstr>Worksheets</lspstr>
<variant>
<i4>1</i4>
<variant>
<vector>
</HeadingPairs>
<TitlesOfParts>
<vector size="1" baseType="lspstr">
<lspstr>Sheet1</lspstr>
</vector>
</TitlesOfParts>
<Company>ACME</Company>
<LinksToDate>false</LinksToDate>
<SharedDoc>false</SharedDoc>
<HyperlinksChanged>false</HyperlinksChanged>
<AppVersion>15.0300</AppVersion>⬡
</Properties>
```

你主要感兴趣的是其中的几个元素：`Application` ①、`Company` ② 和 `AppVersion` 独自。版本本身并没有明显地与 `Office` 版本名称（例如 `Office 2013`、`Office 2016` 等）相关，但该字段与更易读、通用的替代方案之间存在逻辑映射。你开发的代码将维护这种映射关系。

## 定义 metadata 包

在列表 3-20 中，在一个名为 `metadata` 的新包中定义与这些 `XML` 数据集对应的 `Go` 类型，并将代码放在名为 `openxml.go` 的文件中——每个你想要解析的 `XML` 文件对应一个。然后添加一个数据映射和一个方便函数，用于确定与 `AppVersion` 对应的可识别的 `Office` 版本。

```go

type OfficeCoreProperty struct {

  XMLName        string `xml:"coreProperties"`

  Creator        string `xml:"creator"`

  LastModifiedBy string `xml:"lastModified"`

}
```

```go

type OfficeAppProperty struct {

  XMLName     string `xml:"Properties"`

  Application string `xml:"Application"`

  Company     string `xml:"Company"`

  Version     string `xml:"AppVersion"`

}
```

```go

var OfficeVersions = map[string]string{

  "16": "2016",

  "15": "2013",

  "14": "2010",

  "12": "2007",

  "11": "2003",

}
```

```go

func (a *OfficeAppProperty) GetMajorVersion() string {

  tokens := strings.Split(a.Version, ",")

  if len(tokens) < 2 {

    return "Unknown"

  }

  v, ok := OfficeVersions[tokens[0]]

  if !ok {

    return "Unknown"

  }

  return v

}
```

列表 3-20: `Open XML` 类型定义和版本映射 (`/ch-3/binding-metadata/metadata/openxml.go`)

在定义了 `OfficeCoreProperty` 和 `OfficeAppProperty` 类型后，定义一个映射 `OfficeVersions`，用于维护主版本号与可识别发布年份之间的关系 ①。要使用此映射，在 `OfficeAppProperty` 类型上定义一个方法 `GetMajorVersion()` ②。该方法拆分 `XML` 数据的 `AppVersion` 值以获取主版本号 ③，随后使用该值和 `OfficeVersions` 映射来获取发布年份 ④。

## 将数据映射到结构体

现在你已经构建了用于处理和检查感兴趣的 `XML` 数据的逻辑和类型，你可以创建读取相应文件并将内容分配给你的结构体的代码。为此，如列表 3-21 所示，定义 `NewProperties()` 和 `process()` 函数。

```go

func NewProperties(*zip.Reader) (*OfficeCoreProperty, *OfficeAppProperty, error) {

  var coreProps OfficeCoreProperty

  var appProps OfficeAppProperty

  for _, f := range r.File {

    switch f.Name {

    case "docProps/core.xml":

      if err := process(f, &coreProps); err != nil {

        return nil, err

      }

    case "docProps/app.xml":

      if err := process(f, &appProps); err != nil {

        return nil, err

      }

    default:

      continue

    }

  }

  return &coreProps, &appProps, nil

}
```

```go

func process(f *zip.File, prop interface{}) error {

  rc, err := f.Open()

  if err != nil {

    return err

  }

  defer rc.Close()
```
