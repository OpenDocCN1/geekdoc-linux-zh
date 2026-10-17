
显示归档的内容，并验证其中包含的数字签名以及与其关联的文件的加密完整性。这包括检查对象签名证书颁发者的证书是否列在证书数据库中，CA 在对象签名证书上的数字签名是否有效，相关证书是否未过期等等。

### `-verbosity value`
设置 Netscape Signing Tool 在操作过程中生成的信息量。值为 `0`（零）是默认值，提供完整信息。值为 `-1` 会抑制大多数消息，但不包括错误消息。

### `-w archive`
显示归档中任何文件的签名者名称。

### `-x directory`
将指定目录排除在签名之外。请注意，在 Netscape Signing Tool `1.1` 及更高版本中，此选项可以在一个命令行中出现多次，从而可以指定多个要排除的特定目录。

### `-Z`
告诉 `signtool` 不要在数字签名中存储签名时间。如果您希望签名的过期日期与当前日期和时间而不是文件签名时的时间进行检查，则此选项很有用。

### `-Z jarfile`
创建具有指定名称的 JAR 文件。如果您希望 `signtool` 创建 JAR 文件，必须指定此选项；它不会自动创建。如果您不指定 `-Z`，则必须使用外部 ZIP 工具来创建 JAR 文件。`-Z` 选项不能与 `-J` 选项同时使用。如果未将 `-c#` 选项与 `-Z` 选项一起使用，默认压缩值为 `6`。

### 命令文件格式
Netscape Signing Tool 命令文件中的条目具有此通用格式：

`keyword=value`

单行中 `=` 号之前的所有内容都是关键字，从 `=` 号到行尾的所有内容都是值。值可以包含 `=` 号；仅解释该行上的第一个 `=` 号。空行被忽略，但包含关键字和值的行上的空白假定是关键字的一部分（如果在等号之前）或值的一部分（如果在第一个等号之后）。关键字不区分大小写，值通常区分大小写。由于 `=` 号和换行符分隔值，因此它不应该加引号。

### 小节

#### `basename`
- 与 `-b` 选项相同。

#### `compression`
- 与 `-c` 选项相同。

#### `certdir`
- 与 `-d` 选项相同。

#### `extension`
- 与 `-e` 选项相同。

#### `generate`
- 与 `-G` 选项相同。

#### `installScript`
- 与 `-i` 选项相同。

#### `javascriptdir`
- 与 `-j` 选项相同。

#### `html`
- 与 `-J` 选项相同。

#### `certname`
- 证书的昵称，与 `-k` 和 `-l` 选项一样。

`signdir`
要签名的目录，与 `-k` 选项相同。

`list`
与 `-l` 选项相同。值被忽略，但必须存在 `=` 符号。

`listall`
与 `-L` 选项相同。值被忽略，但必须存在 `=` 符号。

`tafile`
与 `-m` 选项相同。

`modules`
与 `-M` 选项相同。值被忽略，但必须存在 `=` 符号。

`optimize`
与 `-o` 选项相同。值被忽略，但必须存在 `=` 符号。

`password`
与 `-p` 选项相同。

`keysize`
与 `-s` 选项相同。

`token`
与 `-t` 选项相同。

`verify`
与 `-v` 选项相同。

`who`
与 `-w` 选项相同。

`exclude`
与 `-x` 选项相同。

`noti`
与 `-z` 选项相同。值被忽略，但必须存在 `=` 符号。

`jarfile`
与 `-Z` 选项相同。

`outfile`
将重定向输出和错误消息的文件名。此选项没有等效的命令行选项。

### 扩展示例
以下示例将执行此操作和那个操作

### 列出可用的签名证书
您使用 `-L` 选项来列出所有可用证书的昵称，并检查哪些是签名证书。

```
signtool -L
using certificate directory: /u/jsmith/..netscape
S Certificates
--------------
BBN Certificate Services
CA Root 1
IBM World Registry CA
VeriSign Class 1 CA - Individual Subscriber
VeriSign, Inc.
GTE CyberTrust Root CA
Upti Group Plc.
Class 4 CA
* Verisign Object Signing Cert
Integreon CA
GTE CyberTrust Secure Server CA
AT&T Directory Services
* test object signing cert
Upti Group Plc.
Class 1 CA
VeriSign Class 1 Primary CA
--------------
Certificates that can be used to sign objects have **s to their left.
```

显示了两个签名证书：Verisign Object Signing Cert 和 test object signing cert。

您使用 `-l` 选项来获取仅包含签名证书的列表，包括每个证书对应的签名 CA。

```
signtool -l
using certificate directory: /u/jsmith/..netscape
Object signing certificates
-------------------------
Verisign Object Signing Cert
Issued by: VeriSign, Inc.
- Verisign, Inc.
Expires: Tue May 19, 1998
test object signing cert
Issued by: test object signing cert (Signtool 1.0 Testing Certificate (960187691))
Expires: Sun May 17, 1998
-------------------------
```

对于包含 CA 的列表，请使用 `-L` 选项。

### 签名文件
- 1. 创建一个空目录。
```
mkdir signdir
```
- 2. 将一些文件放入其中。
```
echo boo > signdir/test.f
```
- 3. 指定您的对象签名证书的名称并签名该目录。
```
signtool -k MySignCert -Z testjar.jar signdir
using key "MySignCert"
using certificate directory: /u/jsmith/..netscape
Generating signdir/META-INF/manifest.mf file..
-> test.f
adding signdir/test.f to testjar.jar
Generating signtool.sf file..
Enter Password or Pin for "Communicator Certificate DB":
adding signdir/META-INF/manifest.mf to testjar.jar
adding signdir/META-INF/signtool.sf to testjar.jar
adding signdir/META-INF/signtool.rsa to testjar.jar
tree "signdir" signed successfully
```
- 4. 测试您刚创建的归档。
```
signtool -v testjar.jar
using certificate directory:
/u/jsmith/\.netscape
archive "testjar.jar" has passed crypto
verification.
status path
--------------------------------
verified
test.f
```

### 使用 Netscape 签名工具配合 ZIP 实用程序
要将 Netscape 签名工具与 ZIP 实用程序一起使用，您的路径环境变量中必须包含该实用程序。建议使用 `zip.exe` 实用程序，而不是 `pkzip.exe`，因为后者无法处理长文件名。在签名后，您可以使用 ZIP 实用程序而不是 `-Z` 选项将签名的归档打包为 JAR 文件：
```
cd signdir
zip -r ../myjar.jar *
adding: META-INF/ (stored 0%)
adding: META-INF/manifest.mf (deflated 15%)
adding: META-INF/signtool.sf (deflated 28%)
adding: META-INF/signtool.rsa (stored 0%)
adding: text.txt (stored 0%)
```

### 生成密钥和证书
