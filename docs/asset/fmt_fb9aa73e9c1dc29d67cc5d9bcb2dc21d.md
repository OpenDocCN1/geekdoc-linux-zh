
一台DNS服务器使用多个区域文件来覆盖DNS的不同组成部分。每个区域使用两个区域文件：主区域文件和反向映射区域文件。区域文件包含该区域内主机的资源记录。反向映射文件包含用于对域名条目进行反向映射的记录，使你能够从IP地址映射到域名。区域文件使用的文件名可以是任意名称。文件名在`named.conf`文件的`zone`语句的`file`条目中指定。如果你的服务器支持多个区域，你可能希望使用一个能表示特定区域的名称。大多数系统使用域名作为区域文件的名称。例如，`mytrek.com`区域会有一个同样名为`mytrek.com`的区域文件。这些文件可以放在名为`zones`或`master`的子目录中。以下示例中使用的区域文件名为`mytrek.com`。反向映射文件可以使用任意名称，但通常使用其对应区域文件中指定的反向IP地址域。例如，对于`mytrek.com`区域文件，反向映射文件可能被称为`192.168.0`，即`mytrek.com`区域文件中定义的`mytrek.com`域的IP地址。该文件将包含域中所有主机地址的反向映射，允许将其主机名地址映射到相应的IP地址。此外，BIND还会为localhost设置一个缓存文件和一个反向映射文件。缓存文件保存着你的名称服务器所连接的根名称服务器的资源记录。缓存文件可以使用任意名称，尽管通常称为`named.ca`。localhost反向映射文件保存着本地回环接口localhost的反向IP资源记录。虽然localhost可以使用任意名称，但它通常命名为`named.local`。

## 互联网区域的区域文件

区域文件包含遵循特定格式的资源记录。文件以定义默认域或包含其他资源记录文件的一般指令开头。接着是单个SOA记录、名称服务器和域资源记录，然后是不同主机的资源记录。注释以分号开头，可以放置在文件中的任何位置。`@`符号就像一个特殊宏，代表记录所应用区域的域名。`@`符号在资源记录或SOA记录的第一个字段中用作该区域的域名。可以使用`*`匹配字符来指定多个名称。资源记录中的第一个字段是其适用的域的名称。如果该字段留空，则会自动使用另一个资源记录中之前显式输入的名称。这样，你可以列出适用于同一主机的多个条目，而无需重复主机名。在此文件中使用的任何主机名或域名，如果未以句点结尾，都会自动附加区域的域名。例如，如果区域的域名是`mytrek.com`，而资源记录中只有名称`rabbit`且没有尾随句点，则会自动附加区域域名，得到`rabbit.mytrek.com`。每当你输入完整的完全限定域名（如`turtle.mytrek.com`）时，请务必包含尾随句点。

## 指令

你还可以使用几个指令来设置全局属性。`$ORIGIN`设置默认域名，用于附加到不以句点结尾的地址名称上。`$INCLUDE`包含一个文件。`$GENERATE`可以生成域名或IP地址仅因迭代数字不同而有所区别的记录。`$ORIGIN`指令通常用于指定在地址记录中使用的根域。请务必包含尾随句点。以下示例将域原点设置为`mytrek.com`，并且`lizard`主机名之后会自动附加该域名。

```
$ORIGIN  mytrek.com.
lizard   IN  A    192.168.0.2
```

## SOA记录

区域文件以SOA记录开头，该记录指定名称服务器运行的机器以及其他规范。`@`符号用作SOA记录的名称，表示区域的域名。在SOA之后，列出名称服务器资源记录（NS）。名称服务器记录的正下方是域本身的资源记录。其后是主机地址（A）、别名（CNAME）和邮件交换器（MX）的资源记录。下一个示例显示了一个示例区域文件，该文件以SOA记录开头，后跟NS记录、域的资源记录，然后是各个主机的资源记录：

```
; Authoritative data for turtle.mytrek.com
@  IN  SOA  turtle.mytrek.com.  hostmaster.turtle.mytrek.com. (
                  93071200  ; Serial number
                  10800    ; Refresh 3 hours
                  3600     ; Retry 1 hour
                  3600000  ; Expire 1000 hours
                  86400 )  ; Minimum 24 hours

                 IN  NS   turtle.mytrek.com.
                 IN  A    192.168.0.1
                 IN  MX  10   turtle.mytrek.com.
                 IN  MX  15   rabbit.mytrek.com.

turtle   IN  A     192.168.0.1
         IN  HINFO  PC-686 LINUX
gopher   IN  CNAME  turtle.mytrek.com.
ftp      IN  CNAME  turtle.mytrek.com.
```

```
www	IN	A	192.168.0.1
rabbit	IN	A	192.168.0.2
lizard	IN	A	192.168.0.3
IN	HINFO	MAC MACOS
localhost	IN	A	127.0.0.1
```

前两行是对使用此区域文件的服务器的注释。请注意，前两行以分号开头。文件中每个资源记录的类均为 IN，表示这些是 Internet 记录。SOA 记录以 @ 符号开头，表示区域的域名。在此示例中，它是 mytrek.com。在此文件中使用的任何主机或域名如果未以句点结尾，则会自动追加此域名。例如，在以下资源记录中，turtle 没有句点，因此自动扩展为 turtle.mytrek.com。rabbit 和 lizard 也是如此。它们被读取为 rabbit.mytrek.com 和 lizard.mytrek.com。另外，在 SOA 中，请注意 hostmaster 的电子邮件地址使用句点而不是 @ 符号；@ 是区域文件中的特殊符号，不能用于其他任何目的。

## Nameserver Record

下一个资源记录指定此区域的名称服务器。在这里，它是 mytrek.com。请注意此资源记录的名称为空。如果名称为空，资源记录将继承前一条记录的名称。在这种情况下，NS 记录继承 SOA 记录中 @ 的值，即其前一条记录。这是区域的域名，NS 记录指定 turtle.mytrek.com 为此区域的名称服务器。

```
IN	NS	turtle.mytrek.com.
```

这里域名是继承的。该条目可以读作如下。请注意域名末尾的尾随句点：

```
mytrek.com. IN NS turtle.mytrek.com.
```

## Address Record

以下地址记录为域名本身设置了一个地址。这通常与名称服务器相同，在本例中为 192.168.0.1（turtle.mytrek.com 的 IP 地址）。这使用户能够引用域名本身，而不是其中的特定主机。随后是一个邮件交换器记录，将域的邮件路由到名称服务器。用户可以向 mytrek.com 域发送邮件，它将被路由到 turtle.mytrek.com。

```
IN	A	192.168.0.1
```

这里域名是继承的。该条目可以读作如下：

```
mytrek.com. IN A 192.168.0.1
```

## Mail Exchanger Record

下一个记录是邮件交换器（MX）记录，列出 turtle.mytrek.com 和 fast.mytrek.com 作为此区域的邮件服务器。你可以为一个主机设置多个邮件交换器记录。可以通过多个主机路由邮件。这些可以在邮件交换器记录中列出，你可以为其设置优先级排名（数字越小排名越高）。在此示例中，如果无法访问 turtle.mytrek.com，其邮件将通过 rabbit.mytrek.com 路由，后者也已设置用于处理 mytrek.com 域的邮件：

```
IN    MX    100    turtle.mytrek.com.
IN    MX    150    rabbit.mytrek.com.
```

再次，域名是继承的。条目可以读作如下：

```
mytrek.com.    IN    MX    100    turtle.mytrek.com.
mytrek.com.    IN    MX    150    rabbit.mytrek.com.
```

## Address Record with Host Name

以下资源记录是一个地址记录（A），将 IP 地址与完全限定域名 turtle.mytrek.com 关联。资源记录名称仅包含 turtle 且没有尾随句点，因此自动扩展为 turtle.mytrek.com。此记录提供了 turtle.mytrek.com 可以映射到的 IP 地址。

```
turtle    IN    A    192.168.0.1
```
