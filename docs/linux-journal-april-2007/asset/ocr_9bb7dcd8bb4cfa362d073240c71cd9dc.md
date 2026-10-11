![](bbox=[0.06, 0.13, 0.49, 0.49])

# Figure 4. Final Master with Dynamic Text Layer

XSLT markup with a text editor. Converting the SVG was a rather simple matter. To make it a true XSLT, only a few lines are required in the header. Listing 1 shows a few lines of the SVG before we modified it. Listing 2 shows the same set of lines with the XSLT markup.

As you can see, there are four new lines. The first new line declares this file an XSLT. The second new line contains an XPath (XML Path Language) expression that matches the root element in our claim data XML. This line tells the XML transform engine where to start reading the XML to do the conversion. The last two new lines simply close the open xml tags.

At this point, the XSLT can be used in conjunction with our claim data XML to produce an SVG. However, the resulting SVG would look just like the SVG did before we modified it. To make it actually show the claim data, we had to go into the XSLT and add all of the XPath expressions to populate the SVG. Because we divided the SVG object into layers, we had to modify only the dynamic text layer. In the SVG XML, the dynamic text layer is nothing more than a series of text tags. Listing 3 shows the text tag for the Patient's City box on our claim form.

When the XSLT is applied to the claim data XML, the value of /claim/patient/address/city will be substituted here. We went through the entire XSLT and added the appropriate XPath expressions where they belonged. In special cases, we also added XPath conditional logic and formatting rules.

# The Claim Data XML

As mentioned previously, all of our claim data was in a database—a Postgres database to be more specific. As we wanted a solution that was not language-specific, we had to devise a way to get the claim data out of the database and into an XML format without depending on a specific programming language. One of my fellow developers had the idea to write a series of PLuGSQL functions to return a single XML string that contained the claim data. His solution was brilliant and fit the bill perfectly. All we needed to do to get the claim data was run one small query with the ID of the claim (Listing 4). The result was well-formatted XML that we used to make claim images.

# Listing 1. A Few Lines of the SVG before Modifying

```
<xml version="1.0" encoding="UTF-8" standalone="no">
<!-- Created with Inkscape (http://www.inkscape.org) -->
<svg
...
</svg>
```

# Listing 2. The Same Set of Lines with the XSLT Markup

```
<xml version="1.0" encoding="UTF-8" standalone="no">
<!-- Created with Inkscape (http://www.inkscape.org) -->
<xsl:stylesheet version="1.0"
xmlns:xsl="http://www.w3.org/1999/XSL/Transform">
<xsl:template match="/claim">
<svg
...
</svg>
</xsl:template>
</xsl:stylesheet>
```

# Listing 3. Text Tag for the Patient's City Box on the Claim Form

```
<text
 xml:space="preserve"
 style="..."
 x="33.237278"
 y="231.77995"
id="textPatientCity"
 sodipodi:linespacing="125.00000%"
 inkscape:label="ttext7272">
<tspan
 sodipodi:role="line"
 d="tspan7274"
 x="33.237278"
 y="231.77995">«xsl:value-of
 select="patient/address/city"/>>«tspan»</tspan></text>
```

# Listing 4. Query with ID of the Claim

```
SELECT  «xml_to_string('01592008a5226')»;
```