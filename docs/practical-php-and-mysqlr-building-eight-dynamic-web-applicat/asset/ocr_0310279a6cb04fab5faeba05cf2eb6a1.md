For the table heading font, you style the text as uppercase (`text-transform`), add some letter spacing (`letter-spacing`), align the text to the center (`text-align`), and set the color to black (`color`).

You also style the top and bottom border of the table heading cells. The top is set to a thick solid gray line, and the bottom border of the cells is set to a slightly darker thin gray line.

# ## SUMMARY

Within this project, the main focus has been on creating a complete stylesheet. The stylesheet you created will be applied to all the projects throughout the rest of the book. The only styles that have been left out are the table styles, because many of the other projects style tables in different ways. The Calendar and Forms projects have very different table styles, for example.

Example A-6 shows the complete stylesheet that is used elsewhere in the book:

**EXAMPLE A-6 The completed stylesheet will prevent the need to create a new CSS file for each project.**

```
```
body {
font-family: "trebuchet ms", verdana, sans-serif;
font-size: 12px;
line-height: 1.5em;
color: #333;
background: #ffffff;
margin: 0;
padding: 0;
text-align: center;
width: 100%;
}

p {
margin-top: 10px;
}

a:link {
text-decoration: none;
color: #000;
}

a:visited {
text-decoration: none;
border-bottom: 1px dotted #369;
color: #000;
}
```
```

*continues*