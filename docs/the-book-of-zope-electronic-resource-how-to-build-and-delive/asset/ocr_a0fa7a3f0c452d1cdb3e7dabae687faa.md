# 2.5.1 Standard Objects

As you have noticed, the root directory contains a number of objects created upon installation of the Zope server. These standard objects ensure a consistent appearance for objects created using Zope, and because they are in the root directory, they can be called by all objects.

# 2.5.1.1 Standard HTML Header and Footer

For example, the standard objects define the header and footer in each text object and standard_html_footer define the inserted into every DTML method and document by default. The code in these files looks like that shown in Listings 2-1 and 2-2.

Listing 2-1: The standard header

```
`<HTML><HEAD><TITLE><html-var title_or_id></TITLE></HEAD><BODY BGCOLOR="FFFFFF">`
```

Listing 2-2: The standard footer

```
<p>
<dt-var ZopeAttributeButton
</p>
</BODY></HTML>
```

These objects define an HTML header and footer. Both can be called at the start and end of DTML methods and documents to embed them in a basic HTML structure; they are missing only the body of the HTML document.

# 2.5.1.2 index_html

The method index_html defines the welcome screen from which you access the Zope management screen, among other screens. It looks like this:

```
<dt-var standard_html_header>
<dt-var zope_quick_start>
<dt-var standard_html_footer>
```

> NOTE: To create a new "home page" on your Zope server, you can modify this method.

# 2.5.1.3 standard_error_message

The method standard_error_message is used to display Zope error messages in a uniform and consistent way. This can be modified to display error messages in any desired format.