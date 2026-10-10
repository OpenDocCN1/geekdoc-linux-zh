
## Honorific

`Honorific` 元素包含如博士或教授或任何附加在名字上的头衔。这仅用于元信息元素，而不用于行内文本。例如，如果你正在使用 `Author` 元素并描写一个拥有博士学位的人，你可以使用 `Honorific` 元素。然而，在文档本身中写博士时，没有必要使用此元素。

`Honorific` 元素使用通用属性。

示例：

```
<author>
<firstname>Kara</firstname>
<surname>Pritchard</surname>
<honorific>Mrs.</honorific>
</author>
```

## IssueNum

`IssueNum` 元素指的是被引用作品或文档本身的期号，取决于其所处的上下文。

`IssueNum` 元素使用通用属性。

示例：

```
<!DOCTYPE article PUBLIC //OASIS//DTD DocBook V4.1//EN>
<article>
<artheader>
  <author>...</author>
  <volum>1</volume>
  <issuenumber>1</issuenumber>
  <pubdate>2001</pubdate>
  <title>...</title>
</artheader>
<para>...</para>
</article>
```

## LegalNotice

`LegalNotice` 元素包含某种类型的法律声明。

`LegalNotice` 元素使用通用属性。

示例：

```
<legalnotice>
<para>Don't reproduce this in any medium or you'll be gnawed to death by angry lawyers.</para>
</legalnotice>
```

## Lineage

`Lineage` 元素的名称具有误导性。它用于指定如 Sr.（父）或 Jr.（子）之类的头衔。

`Lineage` 元素使用通用属性。

示例：

```
<author>
  <firstname>Theodore</firstname>
  <surname>Graddy</surname>
  <lineage>Jr.</lineage>
  <othername>Dad</othername>
</author>
```

## OrgDiv

`OrgDiv` 元素持有公司或机构的部门名称。它仅与 `Affiliation` 元素结合使用。

`OrgDiv` 元素使用通用属性。

示例：

```
<affiliation>
  <jobtitle>Director or Exam Development</jobtitle>
  <orgname>Linux Professional Institute</orgname>
  <orgdiv>Exam Development</orgdiv>
</affiliation>
```

## OrgName

`OrgName` 元素包含机构名称。

`OrgName` 元素使用通用属性。

示例：

```
<orgname>Red Cross</orgname>
```

## OtherAddr

`OtherAddr` 元素持有没有相应元素的地址信息。

`OtherAddr` 元素使用通用属性。

示例：

```
<address>
  Kara Pritchard
  <street>42 Yourstreet C</street>
  <otheraddr>
    <city>...</city>, <state>...</state> <postcode>...</postcode>
  </otheraddr>
</address>
```

## OtherCredit

`OtherCredit` 元素持有关于文档其他贡献者的信息。

`OtherCredit` 元素使用通用属性。

示例：

```
<!DOCTYPE artheader PUBLIC "//OASIS/DTD DocBook V4.1//EN">
<artheader>
```

## Element Reference 293

```
<title>DocBook Publishing</title>
<author>
  <firstname>Joe</firstname>
  <surname>Brockmeier</surname>
</author>
<othercredit>
  <firstname>Kara</firstname>
  <surname>Pritchard</surname>
  <contrib>Tech Editor turned Co-author</contrib>
</othercredit>
</artheader>
```

## OtherName

`OtherName` 元素是一个方便的备用字段，用于列出那些需要包含昵称或中间名的作者姓名。请注意，如果是昵称且你希望以引号形式显示它，则必须这样写。

`OtherName` 元素使用通用属性。

示例：

```
<author>
  <firstname>Kara</firstname>
  <surname>Pritchard</surname>
  <othername>O' Lady</othername>
</author>
```

## PageNums

`PageNums` 元素包含被引用作品的页码信息。

`PageNums` 元素使用通用属性。

示例：

```
<pagenums>55-102</pagenums>
```

## Phone

`Phone` 元素出乎意料地持有一个电话号码。

`Phone` 元素使用通用属性。

示例：

```
<phone>555-555-FAKE</phone>
```

## POB

`POB` 元素持有邮邮箱信息。

`POB` 元素使用通用属性。

示例：

```
<address>
Kara Pritchard
<pob>PO Box 42</pob>
<city>...</city>, <state>CA</state><postcode>...</postcode>
</address>
```

## PostCode

`PostCode` 元素持有邮政编码或其他邮政信息，取决于所在国家。它与 `Address` 元素配合使用。

`PostCode` 元素使用通用属性。

示例：

```
<postcode>80015</postcode>
```

## PubDate

`PubDate` 元素持有关于文档或被引用作品发布日期的信息。

`PubDate` 元素使用通用属性。

示例：

参见 `IssueNum` 示例。

## Publisher

`Publisher` 元素持有被引用作品或当前 `DocBook` 文档的出版者信息。

`Publisher` 元素使用通用属性。

示例：

```
<publisher>
<publishername>Prima Publishing</publishername>
<address>...</address>
</publisher>
```

## PublisherName

`PublisherName` 元素持有出版者的名称。

`PublisherName` 元素使用通用属性。

示例：

参见 `PublisherName` 元素示例。

## Quote

`Quote` 元素持有内联引文。`Quote` 元素用于正文中较的引文，而不是那种从文中独立出来的较长引文。

`Quote` 元素使用通用属性。

示例：

```
<quote>The quick brown fox jumps over the lazy dog.</quote>
```

## SeriesInfo

`SeriesInfo` 元素持有关于系列的信息。

`SeriesInfo` 元素使用通用属性。

示例：

```
<seriesinfo>
  <title>DocBook Series</title>
</seriesinfo>
```

## SeriesVolNums

`SeriesVolNums` 元素持有系列的卷号。

`SeriesVolNums` 元素使用通用属性。

示例：

```
<seriesvolnums>1-5</seriesvolnums>
```

## ShortAffil

`ShortAffil` 元素持有简写的机构名称。

`ShortAffil` 元素使用通用属性。

示例：

```
<shortaffil>LPI</shortaffil>
```

如果你想让 URL 在纯文本或类似格式中呈现，请使用此语法：

```
<link url="http://www.slashdot.org/">http://www.slashdot.org</link>
```

## XRef

`XRef` 元素包含对文档其他部分的引用。

`XRef` 元素接受以下属性：

- `Endterm`. 接受一个 CDATA 值，没有默认值且不是必选的。如果提供了 `Endterm` 值，则该元素将作为链接显示。
- `Linkend`. 接受一个 IDREF 值，没有默认值，但是是必需的。

示例：
