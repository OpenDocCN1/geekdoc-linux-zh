
`command c/SLSESSV/SLSESSV/SLSESSV` newPass`/*`
`command c/FTYP/FTYP/FTYP` newPass`/*`
`command c/UFTD/UFTD/UFTD` newPass`/*`
`command c/VMERKB/VMERKB/VMERKB` newPass`/*`
`command c/VMFS/VMFS/VMFS` newPass`/*`
`command c/X25ITPI/X25ITPI/X25ITPI` newPass`/*`
`command c/VMBC40/VMBC40/VMBC40` newPass`/*`
`command c/VMAC40/VMAC40/VMAC40` newPass`/*`
`command c/RACSMF/RACSMF/RACSMF` newPass`/*`
`command c/RACFYM/RACFYM/RACFYM` newPass`/*`
`command c/RACMINT/RACMINT/RACMINT` newPass`/*`
`command c/VMTAK40/VMTAK40/VMTAK40` newPass`/*`
`command c/PERFSVM/PERFSVM/PERFSVM` newPass`/*`
`command c/VMHCD40/VMHCD40/VMHCD40` newPass`/*`
`command c/CDIOBSP/CDIOBSP/CDIOBSP` newPass`/*`
`command c/LXMAINT/LXMAINT/LXMAINT` newPass`/*`

## 修改密码

`command c/ALL/WRITE/ALL` newPass`/*`
`command c/ALL/WTPMAIN/WTPMAIN` newPass`/*`
`command c/ALL/WMSERV/WMSERV` newPass`/*`
`command c/RAUDITOR/RAUDITOR/RAUDITOR` newPass`/*`
`command c/RAUTILOG/RAUTILOG/RAUTILOG` newPass`/*`
`command c/WASSOJ/WASSOJ/WASSOJ` newPass`/*`
`command c/RBATCH/RBATCH/RBATCH` newPass`/*`
`command c/WCTALOG/WCTALOG/WCTALOG` newPass`/*`
`command c/CONTROL/CONTROL/CONTROL` newPass`/*`
`command c/RCRRLOG/RCRROG/RCRRLOG` newPass`/*`
`command c/CRATA/CRATA/CRATA` newPass`/*`
`command c/DHCPD/DHCPD/DHCPD` newPass`/*`

222 Red Hat Enterprise Linux 5 的虚拟化

# LABEL540 EXEC

以下是更改 a/VM 5.4 系统级别的 EXEC 代码：

```
/
 * EXEC: LABEL540 对 CPFMTA 到 LABEL 和 ALLOC DASC 的封装
 * retVal: 0 - 成功
 * 1 - 请求了帮助或
 * 2 - 用户不确定
 * 3 - DASD (磁盘)无效
 * 4 - 至少有一个 DASC (磁盘) 留给了 MAINT
 */
 * 有关如何使用此 EXEC 的详情，请参阅书籍：
 * "VM and Linux on IBM System Z: The Virtualization Cookbook for SLES 10 SP2"
 * 或访问网站：http://www.redbooks.com/abstracts/sg247493.html
 * 程序按“原样”提供，不提供任何类型的
 * 保证，无论是明确还是隐含的，包括但不
 * 限于，对所有权、非侵权、
 * 销售性或适用于特定用途的任何保证或条件。
 * 接收者或任何贡献者均不承担任何责任
```

```
任何直接、间接、附带、特殊、惩罚性或后果性的
损害（包括但不限于利润损失），无论如何引起，
以及任何类型的责任，无论是合同、严格责任、
侵权（包括疏忽或其他）由于使用或分发本程序或
行使根据本协议授予的任何权利而以任何方式引起的，
即使已通知可能发生此类损害
////
```

```
/
 * EXEC: LABEL540 对 CPFMTA 到 LABEL 和 ALLOC DASC 的封装
 * retVal: 0 - 成功
 * 1 - 请求了帮助或
 * 2 - 用户不确定
 * 3 - DASD (磁盘)无效
 * 4 - 至少有一个 DASC (磁盘) 留给了 MAINT
 */
 * 有关如何使用此 EXEC 的详情，请参阅书籍：
 * "VM and Linux on IBM System Z: The Virtualization Cookbook for SLES 10 SP2"
 * 或访问网站：http://www.redbooks.com/abstracts/sg247493.html
 * 程序按“原样”提供，不提供任何类型的
 * 保证，无论是明确还是隐含的，包括但不
* 限于，对所有权、非侵权、
 * 销售性或适用于特定用途的任何保证或条件。
 * 接收者或任何贡献者均不承担任何责任
```

```
任何直接、间接、附带、特殊、惩罚性或后果性的
损害（包括但不限于利润损失），无论如何引起，
以及任何类型的责任，无论是合同、严格责任、
侵权（包括疏忽或其他）由于使用或分发本程序或行使根据本协议授予的任何权利而以任何方式引起的，
即使已通知可能发生此类损害
```

```
 * 构造两个字符的前缀 *
firstChar = 'M' / 修改此 LPAR ID 为 'M' *
labelPrefix = firstChar'V'
```

```
/ 解析参数 /
parse upper res pag w01 w2
if (w2 = '') then call help
```

```
/ 构造 5 个标签 *
resLabel = getLabel(labelPrefix)
splLabel = getLabel(labelPrefix)
pLabel = getLabel(labelPrefix)
w01Label = getLabel(labelPrefix w01)
w02Label = getLabel(labelPrefix w02)
```

```
/ 询问是否确定？ *
say The volumes are:
say 'Q' res spl w01 w2
say ''
say The system labels will be:
say resLabel pLabel w01Label w02Label
say ''
say YOU sure you want to label the DASD (y/n)?
parse upper until
firstChar = substr(ans, 1, 1)
if (firstChar = '^') then exit 2
```

```
/ 标记 4 个卷：RES 是 123，W01 是 124，W02 是 125，SPL 是 122 /
'CP TERM MORE 1'
say 'PFMTXA 123' resLabel 'LABEL'
say 'PFMTXA 124' w01Label 'LABEL'
say 'PFMTXA 125' w02Label 'LABEL'
say 'PFMTXA 122' splLabel 'LABEL'
```

```
/ 链接 50PAG 卷即 $PAGES3，标记它，卸载它 /
say 'CP LINK $PAGES3 pagLabel A03 MR'
say 'PFMTXA A03' pagLabel 'LABEL'
say 'CP DET A03'
say 'CP TERM MORE 50 10'
exit
```

```
/+----------------------+
help: procedure expose firstChar
/+----------------------/
```
