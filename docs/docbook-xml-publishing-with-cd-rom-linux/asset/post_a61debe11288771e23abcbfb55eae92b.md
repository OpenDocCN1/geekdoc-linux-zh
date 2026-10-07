
If you have a corporate author but you still wish to list authors or contributors to the information, you can add them using the Collab and ColabName elements, as shown in this next example.

```
<!DOCTYPE article PUBLIC-//OASIS//DTD DocBook V4.1//">
<article>
<articleinfo>
<title>A Technical Manual</title>
<corpauthor>Mega-big Corporation</corpauthor>
<colab><collname>John Q. Public</collname></colab>
<colab><collname>Jane Doe</collname></colab>
</articleinfo>
...
</article>
```

Some stylesheets suppress the collaborator information when rendering output, so you might need to modify the stylesheets if you wish to display collaborators as well as the corporate author information. On the other hand, you might wish to suppress it and simply use the information internally so that the people working on a project know who authored it and to whom they should go for further information. If you have a document with 100 authors, it could be just a little cumbersome to include all on a title page.

With larger corporations you might need to assign a publication number to a document, or it might have been contracted by a client as part of a project. If the document has a specific contract or publication number you can use the ContractNum and PubNumber elements, respectively. The ContractSponsor element is used to indicate the client for whom the document is being produced. The next code example shows a document with the ContractNum, ContractSponsor and PubNumber elements. As you can see they're not difficult to use.

```
<!DOCTYPE article PUBLIC-//OASIS//DTD DocBook V4.1//">
<article>
<articleinfo>
<title>A Technical Manual</title>
<corpauthor>Mega-big Corporation</corpauthor>
<contractnum>2001-01-10</contractnum>
<contractsponsor>Bob's Bagel Bonanza</contractsponsor>
<pubnumber>TM-01</pubnumber>
</articleinfo>
...
</article>
```

# Chapter 12: Creating Technical Documents

Again, it depends on the stylesheets that you use whether the ContractNum, ContractSponsor, or PubNumber are displayed when the document is actually rendered. Note these elements are only to be nested within the ArticleInfo or other Info elements. If you refer to the publication number in the body of the document itself, you would not use the PubNumber element.

# Documents Written for Technical Conferences

If you're writing or marking up a paper for a technical conference, there are several elements used to include information about the conference in the meta-information of the document.

The elements are the ConfDate, ConfGroup, ConfNum, ConfSponsor, and ConfTitle. The ConfDate element is used to designate the dates of the conference, and the ConfTitle indicates the name of the conference, and the ConfSponsor is used for the sponsor of the conference document is being presented at. The ConfNum element is used to indicate the number or other designation of a conference. For instance, if you were presenting a paper at ComputerCon X, the markup would look like this, as long as X is the identifier of a particular conference and not part of the permanent name of the conference:

```
<conftitle>ComputerCon</conftitle>
<confnum>X</confnum>
```

The ConfGroup element is used to enclose the other conference informational elements. If you were writing a paper for the NiftyCon 500, sponsored by Bob's Software Slaughterhouse and taking place from April 1, 2001 to April 2, 2001, it would look like this:

```
<!DOCTYPE article PUBLIC "//OASIS//DTD DocBook V4.1//EN">
<article>
<articleinfo>
<title>Writing Code Makes Me Happy</title>
<author>
<firstname>John</firstname>
<surname>Doe</surname>
</author>
<confgroup>
<confname>NiftyCon</confname>
<confnum>500</confnum>
<confdates>April 1, 2001 - April 2, 2001</confdates>
<confspensor>Bob's Software Slaughterhouse</confspensor>
</configgroup>
<articleinfo>
...
</article>
```

Remember, the Conf elements are meta-information. The default stylesheets that come with SGMILTools will suppress the Conf elements so that the information does not show up when the document is rendered.

# # # Making a man-Style Reference Page

If you've used Linux, one of the BSD variants or any UNIX-style operating system, you've no doubt the man command to read up on a system utility or program. In this section you will walk you through creating a reference page like the manual pages you all know and love.

Look at the markup for a simple reference entry. Then, it will be broken down so that it is easier to understand.

```
<!DOCTYPE REFERENCE PUBLIC "OASIS//DTD DocBook V4.1//EN">
<reference> <title>Reference Example</title>
<refentry>
<refmeta>
<refentrytitle>Example</refentrytitle>
</refmeta>
<refnamdiv>
<refname>Example</refname>
<refpurpose>Provides an example of the Reference and RefEntry elements</refpurpose>
</refnamdiv>
<refsect1><title>Example Text</title>
<para>This is where you would find descriptive text about the subject of the RefEntry element</para>
</refsect1>
</refentry>
</reference>
```

The Reference element might seem like it is misnamed at first. Although you might expect to use the Reference element to create a Reference term, the Reference element isn't used for a specific reference term. Instead it is used to create a reference section that holds a number of RefEntry elements. Each RefEntry element is an individual reference entry, similar to a man page. it could be used to hold just one RefEntry element, as showed in this example, but usually it would be used for a collection of RefEntry elements.

The RefEntry element is not restricted to use with the Reference element. it can be used nearly anywhere in a document.

The RefMeta element holds the meta-information about the RefEntry element, particularly the title of the RefEntry, which is included within the RefEntryTitle element.

The RefS1 element is similar to the Sect1 element, except that it is specific to the RefEntry element. There are three levels of RefS element, RefS1 through RefS3. As with the Sect1 element, the RefS elements do not hold content. Figure 12.1 shows the RefEntry rendered in HTML.![](img/81f56bf497dbf7f7582072400d12cb42_259_0)

# # # # Including Code

When writing a technical document, you might want to include some samples so the reader can follow along. However, the ProgramListing element in DocBook is designed to preserve whitespace. For instance, if you need to include some code, it should look like this:

```
<para>
<programlisting>
&lt;php echo "The Current Date and Time is &nbsp;&br&gt;";
echo date("g:i A 1, F j Y.");

// g = the hour, in 12-hour format
// i = minutes
// A = print AM or PM, depending
// 1 = print the day of the week
// F = print the month
// j = print the day of the month
// Y = print the year - all four digits

&gt;
&lt;?php echo "Hello, World!";&gt;
</programlisting>
</para>
```

You might have guessed by now that when you render a document from DocBook into HTML that the < and > characters are automatically converted into &lt; and &gt;, or their numeric equivalent, &#60; and &#62; so that they'll display properly in a browser.

# Chapter 12: Creating Technical Documents

Luckily, there's a solution. When you have a code sample that you want the DocBook parser to ignore any markup that looks like markup, you can create a CData section under the ProgramListing element. The CData section is declared like this:

```
<!DOCTYPE article PUBLIC "-//OASIS//DTD DocBook V4.1//EN">
<article>
<title>Programlisting</title>
<programlisting>
<![CDATA[
<?php echo "The Current Date and Time is &nbsp;<br>";
echo date("g:i A 1, F j Y.");

// g = the hour, in 12-hour format
// i = minutes
// A = print AM or PM, depending...
// 1 = print the day of the week
// F = print the month
// j = print the day of the month
// Y = print the year - all four digits

?>
<?php echo "Hello, World!";?>
</programlisting>
</article>
```

It looks almost the same, but you get to avoid hassling with the &lt; &gt; to produce the < and > characters. Using a CData section is especially useful when you're writing documents about DocBook, HTML, XML or other markup languages that use tags similar to DocBook.

> You might have guessed by now that when you render a document from DocBook into HTML that the < and > characters are automatically converted into &lt; and &gt;, or their numeric equivalent, &#60; and &#62; so that they'll display properly in a browser.

![](img/81f56bf497dbf7f7582072400d12cb42_261_0.png)
