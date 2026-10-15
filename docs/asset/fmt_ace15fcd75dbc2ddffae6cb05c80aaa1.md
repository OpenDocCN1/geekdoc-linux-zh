
`-N increment` 标志会自动递增 SOA 记录中的序列号，这样你就不会忘记了。你也可以指定值 `unixtime` 将序列号更新为当前 UNIX 时间（自 1970 年 1 月 1 日以来的秒数），或指定值 `keep` 以防止 `dnssec-signzone` 修改原始序列号。序列号在已签名的区域文件中递增，但在原始区域文件中不会递增。

下面是一个使用上面生成的密钥的详细示例：

```
$ sudo dnssec-signzone -o example.com -N increment
-k Kexample.com+005+00682 example.com Kexample.com+005+23301
```

签名文件按字母顺序排序，并包含我们手动添加的 DNSKEY 记录以及签名过程中生成的 RRSIG 和 NSEC 记录。区域的序列号已被递增。

如果你使用 `NSEC3RSASHA1` 算法生成密钥，则会如上所述签名区域，但使用 `-3 salt` 标志。

`dnssec-signzone` 的一些其他有用选项是

- `-g` 生成要包含在父区域中的 DS 记录
- `-I` 生成 DLV 记录以在父区域未签名时使用
- `-s start-time` 设置签名生效的时间
- `-e end-time` 设置签名过期的时间
- `-t` 打印统计信息

签名有效期的日期可以表示为格式为 `yyyymmddhhmmss` 的绝对时间，或表示为相对于现在的格式为 `+N` 的时间，其中 N 以秒为单位。默认签名有效期为从过去一小时到未来 30 天。这里有一个示例，我们指定签名应有效期至 2010 日历年结束：

```
$ dnssec-signzone -N increment -e 20101231235959 example.com
```

在 NSD 下，签名区域的语法为

```
ldns-signzone [-o zonename] zonename key [key ...]
```

你只需列出两个密钥，让 `ldns-signzone` 判断哪个是 KSK，哪个是 ZSK。例如：

```
$ sudo ldns-signzone example.com Kexample.com+005+00682 Kexample.com+005+23301
```

与 `dnssec-signzone` 一样，你可以使用 `-e yyyymmdd` 标志设置签名的过期日期。要为签名间隙生成 NSEC3 记录而不是 NSEC 记录，请使用标志 `-n -s salt`。

### 区域签名

已签名的区域文件通常比原始区域大四到十倍，而且你所有漂亮的逻辑排序都会丢失。如下一行

```
mail-relay                         A       63.173.189.2
```

变成多行：

```
mail-relay.example.com.     57600  A       63.173.189.2
                              57600  RRSIG   A 3 5 57600 20090722234636 (
                                      20090622234636 23301 example.com.
                                      Y7s9jDWWyuXv0zeUJ7zGRdFC1+rzU8cLiw0ev
                                      OI2TGfLbhsRgjfkpEYVUrBU7kVVRNgUEYWx
                                      d2RSKDJ9QzRQ+W== )
                              3600   NSEC    mail-relay.example.com. A RRSIG NSEC
                              3600   RRSIG   NSEC 5 3 3600 20090722234636 (
                                      20090622234636 23301 example.com.
                                      42Qrx8vpoChsGPsePr0BMZTwifES5WK+40
                                      WNsN84hF0notymRxZRIZypqZWzLlPBZAUJ7R
                                      HPh8LbDQcmQZYw== )
```

从实际角度来看，已签名的区域文件不再可供人阅读，并且由于 RRSIG 和 NSEC 或 NSEC3 记录，无法手工编辑。内部没有用户可维修的部件！

除 DNSKEY 记录外，每个资源记录集（同一名称的同类型资源记录）都会得到 ZSK 的一个签名。DNSKEY 资源记录由 ZSK 和 KSK 两者签名，因此它们有两个 RRSIG。签名的 base-64 表示以所需的等号结尾，使长度成为 4 的倍数。

为了在后续示例中更清晰，我们假设区域文件以区域命名，并且区域文件和密钥文件位于同一目录。在现实生活中，显式指定密钥文件实际上是一个好主意，尤其是在你轮换密钥并且需要确保命令使用正确的密钥时。

一旦你的区域已签名，只需将你的名称服务器指向已签名的区域文件即可。如果你使用 BIND，请查找 `named.conf` 中对应每个区域的区域语句，并将 `file` 参数从 `example.com` 改为 `example.com.signed`。对于 NSD，对应的配置文件是 `nsd.conf`，你需要查找 `zonefile` 行。

最后，重新启动名称服务器守护进程，告诉它重新读取其配置文件。对于 BIND，执行 `sudo rndc reconfig` 然后执行 `sudo rndc flush`。对于 NSD，尝试 `sudo nsd reconfig` 然后执行 `sudo nsd restart`。

我们现在正在提供一个 DNSSEC 签名的区域！要进行更改，你可以编辑原始未签名的区域或已签名的区域，然后重新签名区域。编辑已签名的区域在后勤上有点噩梦，但比重新签名整个区域快得多。务必删除与你更改的记录对应的 RRSIG 记录。你可能希望对未签名的区域做相同的更改以避免版本偏差。

![](img/14d78e3cecac4581d37024baf1e94cca_707_0.png)

如果将一个已签名的区域作为参数传递给 `dnssec-signzone` 或 `ldns-signzone`，任何未签名的记录都会被签名，并且任何即将到期的记录的签名都会被续期。“即将到期”被定义为有效期已过四分之三。重新签名通常会导致更改，因此请手动递增区域的序列号，或者在使用 BIND 时，在 `dnssec-signzone` 命令行上使用 `-N increment` 子句自动递增区域的序列号。

这就是 DNSSEC 配置本地部分的全部内容。剩下的棘手问题是如何将我们这个安全的 DNS 孤岛连接到 DNS 层次结构中其他受信任的、已签名的部分。我们要么需要将我们的 DS 记录放入已签名的父区域，要么需要使用域旁路验证变通方法。下一节将介绍这些任务。

### DNSSEC 信任链

继续以我们的示例 DNSSEC 设置为例，`example.com` 现在已签名，并且其名称服务器已启用 DNSSEC。这意味着在查询时它们使用 EDNS0，即扩展 DNS 协议，并在数据包的 DNS 头中设置 DNSSEC 感知选项。当收到设置了该位的查询时，它们会在响应中包含签名数据。

接收到签名响应的客户端可以通过使用适当的公钥检查记录的签名来验证响应。但它是从区域自身的 DNSKEY 记录获取该密钥的，如果你仔细想想，这就很可疑。有什么能阻止冒名者同时提供伪造的记录和用于验证它们的伪造公钥呢？

这个问题有几种可能的答案。你的站点必须至少实现其中一种；否则，你所有的 DNSSEC 工作都将付诸东流。

规范的解决方案是，你向父区域提供一条 DS 记录以包含在其区域文件中。由于 DS 记录来自父区域，因此它由父区域的私钥认证。如果客户端信任你的父区域，那么它应该信任父区域的 DS 记录准确反映了你的区域的公钥。

父区域反过来由其父区域认证，以此类推，直到根。当 DNSSEC 完全部署时，你唯一需要事先知道的密钥就是用于签名根的公钥，该公钥可以放在启动整个 DNS 进程的根提示文件中。

如果你足够幸运拥有一个已签名的父区域，只需向父区域的管理员提供一条 DS 记录和用于签名它的密钥签名 DNSKEY 即可。BIND 的 `dnssec-signzone` 的 `-g` 标志会生成名为 `dsset-domain` 和 `keyset-domain` 的文件，可以安全地交付给你的父区域以直接添加到父区域的区域文件中。同样，NSD 的 `ldns-keygen` 在生成密钥时会在 `.ds` 文件中生成所需的 DS 记录，并在 `.key` 文件中生成 DNSKEY 记录。请注意
