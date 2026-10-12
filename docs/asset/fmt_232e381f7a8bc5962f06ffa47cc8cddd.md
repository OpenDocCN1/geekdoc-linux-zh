
# 列表 686 - 用于检测已注册服务主体名称的 PowerShell 脚本

此搜索返回了若干结果，尽管可以进一步过滤，但我们很容易发现相关信息：

| 名称 | 值 |
| ----- | ----- |
| givenname | {iis_service} |
| samaccountname | {iis_service} |
| cn | {iis_service} |
| pwdlastset | {131623309820953450} |
| whencreated | {05/02/2018 19.03.02} |
| badpwdcount | {0} |
| displayname | {iis_service} |
| lastlogon | {131624786130434963} |
| samaccounttype | {805306368} |
| countrycode | {0} |
| objectguid | {201 74 156 103 125 89 254 67 146 40 244 7 212 176 32 11} |
| usnchanged | {28741} |
| whenchanged | {07/02/2018 12.08.56} |
| name | {iis_service} |
| objectsid | {1 5 0 0 0 0 0 5 21 0 0 0 202 203 185 181 144 182 205 192 58 2} |
| logoncount | {3} |
| badpasswordtime | {0} |
| accountexpires | {9223372036854775807} |
| primarygroupid | {513} |
| objectcategory | {CN=Person,CN=Schema,CN=Configuration,DC=corp,DC=com} |
| userprincipalname | {iis_service@corp.com} |
| useraccountcontrol | {590336} |
| dscorepropagationdata | {01/01/1601 00.00.00} |
| serviceprincipalname | {HTTP/CorpWebServer.corp.com} |
| distinguishedname | {CN=iis_service,OU=ServiceAccounts,OU=CorpUsers,DC=corp,DC=com} |
| objectclass | {top, person, organizationalPerson, user} |
| usncreated | {12919} |
| lastlogontimestamp | {131624773644330799} |
| adspath | {LDAP://CN=iis_service,OU=ServiceAccounts,OU=CorpUsers,DC=corp,DC=com} |

# 列表 687 - 服务主体名称搜索的输出

根据输出，其中一个属性名 `samaccountname` 被设置为 `iis_service`，表明存在 Web 服务器，并且 `serviceprincipalname` 被设置为 `HTTP/CorpWebServer.corp.com`。所有这一切似乎都表明存在一个 Web 服务器。

让我们尝试使用 `nslookup` 解析 `CorpWebServer.corp.com`。

```powershell
PS C:\Users\offsec.CORP> nslookup CorpWebServer.corp.com

Server: Unknown

Address: 192.168.1.110

Name: corpwebserver.corp.com

Address: 192.168.1.110
```
