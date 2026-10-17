
设置要使用的配置文件。默认值为`/etc/pam_pkcs11/pam_pkcs11.conf`。

由于它使用与`pam_pkcs11`相同的配置文件，因此所有`pam_pkcs11`选项也可用。请注意，其中一些选项在非 PAM 环境中没有意义，因此将被忽略。例如，映射器选项（`mapfile`, `ignorecase`）对证书内容没有影响，因此它们也将被忽略。

### 返回值

成功时，`pkcs11_inspect`在标准输出上打印为映射器找到的所有证书内容，并返回`0`。

出错时返回`1`。

### 文件

`/etc/pam_pkcs11/pam_pkcs11.conf`

### 示例

以标准方式运行此程序，请将智能卡插入读卡器并输入：

```
pkcs11_inspect
```

或者，您可以指定选项：

```
pkcs11_inspect debug config_file=${HOME}/.pam_pkcs11.conf
```

### 作者

- Juan Antonio Martinez

### 另请参阅

`(8)`, `(1)` PAM-PKCS11 用户手册

### pkcs11_listcerts

### 名称

`pkcs11_listcerts` - 智能卡 PKCS#11 证书列表

### 语法

```
pkcs11_listcerts [debug]
```

### 描述

`pkcs11_listcerts`显示所有证书。

### 选项

- `debug`

  启用调试输出。

### 作者

- Juan Antonio Martinez

### 另请参阅

`(8)` PAM-PKCS11 用户手册

### pkcs11_setup

### 名称

`pkcs11_setup` - 智能卡 PKCS#11 设置

### 语法

```
pkcs11_setup [list_modules] [debug] [use_module[=<module_name>]] [ins_action[=<executable,executable,...>]] [rm_action[=<executable,executable,...>]]
```

### 描述

`pkcs11_setup`显示所有证书。

### 选项

- `debug`

  启用调试输出。

- `list_modules`

  列出在`/etc/pam_pkcs11/pam_pkcs11.conf`中可用且已配置的模块。

- `use_module`

  显示`pam_pkcs11`使用的模块。

### 作者

- Juan Antonio Martinez

### 另请参阅

`(8)` PAM-PKCS11 用户手册

### PKCS12

### 名称

`pkcs12` - PKCS#12 文件实用工具

### 概要

```
openssl pkcs12 [-export] [-chain] [-inkey filename] [-certfile filename] [-name name] [-caname name] [-in filename] [-out filename] [-noout] [-nomacver] [-nocerts] [-clcerts] [-cacerts] [-nokeys] [-info] [-des] [-des3] [-idea] [-aes128] [-aes192] [-aes256] [-camellia128] [-camellia192] [-camellia256] [-nodes] [-noiter] [-maciter] [-nomaciter] [-nomac] [-twopass] [-descert] [-certpbe] [-keypbe] [-macalg digest] [-keyex] [-keybag] [-password arg] [-passin arg] [-passout arg] [-rand file(s)] [-CAfile file] [-CApath dir] [-CSP name]
```

### 描述

`pkcs12`命令允许创建和解析 PKCS#12 文件（通常称为`PFX`文件）。PKCS#12 文件被包括 Netscape、`MSIE`和 MS Outlook 在内的多个程序使用。

### 命令选项

选项很多；其中一些选项的含义取决于正在创建还是解析 PKCS#12 文件。默认情况下，解析 PKCS#12 文件。通过使用`export`选项（见下文）可以创建 PKCS#12 文件。

#### 解析选项

- `-in filename`

  指定要解析的 PKCS#12 文件的文件名。默认使用标准输入。

- `-out filename`

  写入证书和私钥的文件名，默认为标准输出。它们都以 PEM 格式写入。

- `-passin arg`

  PKCS#12 文件（即输入文件）的密码来源。有关`arg`格式的信息，请参阅`(1)`中的 PASS PHRASE ARGUMENTS 部分。

- `-passout arg`

  用于加密输出私钥的密码短语来源。有关`arg`格式的信息，请参阅`(1)`中的 PASS PHRASE ARGUMENTS 部分。

- `-password arg`

  对于`-export`，`-password`等同于`-passout`。否则，`-password`等同于`-passin`。

- `-noout`

  此选项禁止将 PKCS#12 文件中的密钥和证书输出到输出文件。

- `-clcerts`

  仅输出客户端证书（不输出 CA 证书）。

- `-cacerts`

  仅输出 CA 证书（不输出客户端证书）。

- `-nocerts`

  完全不输出证书。

- `-nokeys`

  不输出私钥。

- `-info`

  输出有关 PKCS#12 文件结构、使用的算法和迭代次数的附加信息。

- `-des`

  使用 DES 在输出前加密私钥。

- `-des3`

  使用三重 DES 在输出前加密私钥，这是默认设置。

- `-idea`

  使用 IDEA 在输出前加密私钥。

- `-aes128`, `-aes192`, `-aes256`

  使用 AES 在输出前加密私钥。

- `-camellia128`, `-camellia192`, `-camellia256`

  使用 Camellia 在输出前加密私钥。

- `-nodes`

  完全不对私钥进行加密。

- `-nomacver`

  不要在读取文件之前尝试验证完整性 MAC。

- `-twopass`

  为完整的完整性和加密密码提示分别输入：大多数软件总是假设这两个密码相同，因此此选项将使此类 PKCS#12 文件无法读取。

#### 文件创建选项

- `-export`

  此选项指定将创建 PKCS#12 文件而不是解析文件。

- `-out filename`

  指定写入 PKCS#12 文件的文件名。默认使用标准输出。

- `-in filename`

  从中读取证书和私钥的文件名，默认使用标准输入。它们都必须采用 PEM 格式。顺序无关紧要，但必须存在一个私钥及其对应的证书。如果存在额外的证书，它们也将包含在 PKCS#12 文件中。

- `-inkey filename`

  读取私钥的文件。如果不存在，则输入文件中必须存在私钥。

- `-name friendlyname`

  指定证书和私钥的“友好名称”。此名称通常由导入文件的软件在列表框中显示。

- `-certfile filename`

  读取额外证书的文件名。

- `-caname friendlyname`

  指定其他证书的“友好名称”。此选项可多次使用，以按出现顺序指定所有证书的名称。Netscape 忽略其他证书的友好名称，而 MSIE 则显示它们。

- `-pass arg`, `-passout arg`

  PKCS#12 文件（即输出文件）的密码来源。有关`arg`格式的更多信息，请参见`(1)`中的`PASS PHRASE ARGUMENTS`部分。

- `-passin password`

  用于解密任何输入私钥的密码短语来源。有关`arg`格式的更多信息，请参见`(1)`中的`PASS PHRASE ARGUMENTS`部分。

- `-chain`

  如果存在此选项，则将尝试包含用户证书的整个证书链。标准 CA 存储用于此搜索。如果搜索失败，则被视为致命错误。

- `-descert`

  使用三重 DES 加密证书，这可能会使某些“出口级”软件无法读取 PKCS#12 文件。默认情况下，私钥使用三重 DES 加密，证书使用 40 位 RC2 加密。

- `-keypbe alg`, `-certpbe alg`
