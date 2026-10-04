```
index_html
another_page
Folder 1
acl_users
standard_error_message
standard_html_header
standard_html_footer
/(Raat Folder)
```

Figure 4-5: The namespace stack of the hierarchy in Figure 4-4

> > It is generally considered good practice to surround all attribute values with quotation marks in DTML unless you have a specific reason not to, because unquoted values are sometimes treated differently by certain DTML tags, such as dtml-let.

The resulting structure is

```
<dtml-Tagname Attribute="Value" Attribute2="value" ...>
```

For example, the following code displays in uppercase letters the name of the user accessing the document containing this line.

```
<dtml-var name="AUTHENTICATED USER" capitalize>
```

In this example, the first attribute, called the name attribute, is assigned the variable AUTHENTICATED_USER as its value. The second attribute, capitalize (which is responsible for displaying the username with its first letter capitalized), requires no value and as a result has no value assigned to it.

# 4.2.1 Empty and Non-Empty Tags

The example above is known as an empty tag because it stands alone; it encloses no text between itself and an end tag. Non-empty DTML tags (also known as container block tags) contain a tag body between start and end tags.

The start tag (Line 1) follows the attribute structure described above. The end tag (Line 3) is similar except that it contains no attributes and the opening-angle bracket is followed by a forward slash: