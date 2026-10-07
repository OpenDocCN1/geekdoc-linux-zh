
# IssueNum

IssueNum element refers to the issue number of a cited work or the document itself, depending on the context in which it is used.

The IssueNum element uses common attributes.

Example:

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

# LegalNotice

The LegalNotice element contains a legal notice of some type.

The LegalNotice element uses common attributes.

Example:

```
<legalnotice>
<para>Don't reproduce this in any medium or you'll be gnawed to death by angry lawyers.</para>
</legalnotice>
```

# Lineage

The Lineage element name is misleading. It designates titles such as Sr. or Jr.

The Lineage element uses common attributes.

Example:

```
<author>
  <firstname>Theodore</firstname>
  <surname>Graddy</surname>
  <lineage>Jr.</lineage>
  <othername>Dad</othername>
</author>
```

# OrgDiv

The OrgDiv element holds the division name of a company or organization. It is used only in conjunction with the Affiliation element.

The OrgDiv element uses common attributes.

Example:

```
<affiliation>
  <jobtitle>Director or Exam Development</jobtitle>
  <orgname>Linux Professional Institute</orgname>
  <orgdiv>Exam Development</orgdiv>
</affiliation>
```

# OrgName

The OrgName element contains the name of an organization.

The OrgName element uses common attributes.

Example:

```
<orgname>Red Cross</orgname>
```

# OtherAddr

The OtherAddr element holds address information for which there are no appropriate elements.

The OtherAddr element uses common attributes.

Example:

```
<address>
  Kara Pritchard
  <street>42 Yourstreet C</street>
  <otheraddr>
    <city>...</city>, <state>...</state> <postcode>...</postcode>
  </otheraddr>
</address>
```

# OtherCredit

The OtherCredit element holds information about other contributors to a document.

The OtherCredit element uses common attributes.

Example:

```
<!DOCTYPE artheader PUBLIC "//OASIS/DTD DocBook V4.1//EN">
<artheader>
```

# Element Reference 293

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

# OtherName

The OtherName element is a handy catchall for use when listing author names who have nicknames or middle names that should be included. Note that if it is a nickname and you want to have the nickname appear in quotes, you must write it as such.

The OtherName element uses common attributes.

Example:

```
<author>
  <firstname>Kara</firstname>
  <surname>Pritchard</surname>
  <othername>O' Lady</othername>
</author>
```

# PageNums

The PageNums element contain page number information for a cited work.

The PageNums element uses common attributes.

Example:

```
<pagenums>55-102</pagenums>
```

# Phone

The Phone element holds, surprisingly, a phone number.

The Phone element uses common attributes.

Example:

```
<phone>555-555-FAKE</phone>
```

# POB

The POB element holds post office box information.

The POB element uses common attributes.

Example:

```
<address>
Kara Pritchard
<pob>PO Box 42</pob>
<city>...</city>, <state>CA</state><postcode>...</postcode>
</address>
```

# PostCode

The PostCode element holds a Zip code or other postal code information, depending on the country. It is used with the Address element.

The PostCode element uses common attributes.

Example:

```
<postcode>80015</postcode>
```

# PubDate

The PubDate element holds information about the publication date of a document or cited work.

The PubDate element uses common attributes.

Example:

See IssueNum example.

# Publisher

The Publisher element holds information about a publisher of a cited work or the current DocBook document.

The Publisher element uses common attributes.

Example:

```
<publisher>
<publishername>Prima Publishing</publishername>
<address>...</address>
</publisher>
```

# PublisherName

The PublisherName element holds the name of the publisher.

The PublisherName element uses common attributes.

Example:

See PublisherName element example.

# Quote

The Quote element holds a quotation used in-line. The Quote element is used for shorter quotations that appear in the text, not longer quotations that are broken out from the text, such as.

The Quote element uses common attributes.

Example:

```
<quote>The quick brown fox jumps over the lazy dog.</quote>
```

# SeriesInfo

The SeriesInfo element holds information about a series.

The SeriesInfo element uses common attributes.

Example:

```
<seriesinfo>
  <title>DocBook Series</title>
</seriesinfo>
```

# SeriesVolNums

The SeriesVolNums element holds volume numbers for a series.

The SeriesVolNums element uses common attributes.

Example:

```
<seriesvolnums>1-5</seriesvolnums>
```

# ShortAffil

The ShortAffil element holds an abbreviated affiliation name.

The ShortAffil element uses common attributes.

Example:

```
<shortaffil>LPI</shortaffil>
```
