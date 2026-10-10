
signdir

要签名的目录，与 -k 选项相同。

list

与 -l 选项相同。值被忽略，但必须存在 = 符号。

listall

与 -L 选项相同。值被忽略，但必须存在 = 符号。

tafile

与 -m 选项相同。

modules

与 -M 选项相同。值被忽略，但必须存在 = 符号。

optimize

与 -o 选项相同。值被忽略，但必须存在 = 符号。

password

与 -p 选项相同。

keysize

与 -s 选项相同。

token

与 -t 选项相同。

verify

与 -v 选项相同。

who

与 -w 选项相同。

exclude

与 -x 选项相同。

noti

与 -z 选项相同。值被忽略，但必须存在 = 符号。

jarfile

与 -Z 选项相同。

outfile

将重定向输出和错误消息的文件名。此选项没有等效的命令行选项。

## 扩展示例

以下示例将执行此操作和那个操作

### 列出可用的签名证书

您使用 -L 选项来列出所有可用证书的昵称，并检查哪些是签名证书。

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

您使用 -l 选项来获取仅包含签名证书的列表，包括每个证书对应的签名 CA。

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

对于包含 CA 的列表，请使用 -L 选项。

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

## 使用 Netscape 签名工具配合 ZIP 实用程序

要将 Netscape 签名工具与 ZIP 实用程序一起使用，您的路径环境变量中必须包含该实用程序。建议使用 zip.exe 实用程序，而不是 pkzip.exe，因为后者无法处理长文件名。在签名后，您可以使用 ZIP 实用程序而不是 -Z 选项将签名的归档打包为 JAR 文件：

```
cd signdir
zip -r ../myjar.jar *
adding: META-INF/ (stored 0%)
adding: META-INF/manifest.mf (deflated 15%)
adding: META-INF/signtool.sf (deflated 28%)
adding: META-INF/signtool.rsa (stored 0%)
adding: text.txt (stored 0%)
```

## 生成密钥和证书

signtool 选项 -G 生成新的公钥-私钥对和证书。它接受新证书的昵称作为参数。新生成的密钥和证书将安装到 -d 选项指定目录中的密钥和证书数据库中。在 Netscape 签名工具的 NT 版本中，必须将 -d 选项与 -G 选项一起使用。在 Unix 版本的 Netscape 签名工具中，省略 -d 选项会使工具将密钥和证书安装到 Communicator 的密钥和证书数据库中。在所有情况下，证书都会输出到一个名为 x509.cacert 的文件，其 MIME 类型为 application/x-x509-ca-cert。

证书包含关于其标识实体的标准信息，例如通用名称和组织名称。当您使用 -G 选项运行命令时，Netscape 签名工具会提示您输入这些信息。但是，对于测试证书，所有请求的字段都是可选的。如果您没有输入通用名称，工具将提供一个默认名称。在以下示例中，用户输入以粗体显示：

```
signtool -G MyTestCert
using certificate directory: /u/souser/\.netscape
Enter certificate information. All fields are optional. Acceptable characters are numbers, letters, spaces, and apostrophes.
certificate common name: Test Object Signing Certificate
organization: Netscape Communications Corp.
organization unit: Server Products Division
state or province: California
country (must be exactly 2 characters): US
username: souser
email address: 
Enter Password or Pin for "Communicator Certificate DB": 
[Password will not echo]
generated public/private key pair
certificate request generated
certificate has been signed
certificate "MyTestCert" added to database
Exported certificate to x509.raw and x509.cacert.
```

证书信息从标准输入读取。因此，在某些操作系统中，可以使用重定向运算符 (<) 从文件读取信息。为了创建用于此目的的文件，按顺序将每个七个输入字段输入在单独的行上。确保最后一行末尾有一个换行符。然后按照以下方式运行 signtool，将标准输入重定向到您的文件：

```
signtool -G MyTestCert < inputfile
```

提示会在屏幕上显示，但响应将自动从文件读取。除非您使用 -p 选项在命令行上提供密码，否则密码仍将从控制台读取。

### 使用 -M 选项列出智能卡

您可以使用 -M 选项列出 signtool 可用的 PKCS #11 模块，包括智能卡：

```
signtool -d "c:\netscape\users\jsmith" -M
using certificate directory: c:\netscape\users\jsmith
Listing of PKCS11 modules
--------------------------
1. Netscape Internal PKCS #11 Module
(this module is internally loaded)
slots: 2 slots attached
status: loaded
slot: Communicator Internal Cryptographic Services Version 4.0
token: Communicator Generic Crypto Svcs
slot: Communicator User Private Key and Certificate Services
token: Communicator Certificate DB
2. CryptoS
(this is an external module)
DLL name: core32
slots: 1 slots attached
status: loaded
slot: Litronic 210
token: ---
```

### 使用 Netscape 签名工具和智能卡签名文件

signtool 命令通常接受 -k 选项的参数以指定签名证书。要使用智能卡进行签名，您只需提供证书的完整限定名称。

要在运行 Communicator 时查看完整的证书限定名称，请单击导航器中的 Security（安全性）按钮，然后单击左侧框架中 Certificates（证书）下的 Yours（您的）。完整限定名称的格式为 smartcard:certificate，例如 "MyCard:My Signing Cert"。您按如下方式使用此名称与 -k 参数配合使用：

```
signtool -k "MyCard:My Signing Cert" directory
```

### 验证 FIPS 模式

使用 -M 选项验证您正在使用 FIPS-140-1 模块。

```
signtool -d "c:\netscape\users\jsmith" -M
using certificate directory: c:\netscape\users\jsmith
Listing of PKCS11 modules
---------------------
1. Netscape Internal PKCS #11 Module
(this module is internally loaded)
slots: 2 slots attached
status: loaded
slot: Communicator Internal Cryptographic Services Version 4.0
token: Communicator Generic Crypto Svcs
slot: Communicator User Private Key and Certificate Services
token: Communicator Certificate DB
-----------------
```

这个 Unix 示例表明 Netscape 签名工具正在使用 FIPS-140-1 模块：

