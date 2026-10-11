Inside a stylesheet, a series of blocks apply style elements to different parts of the HTML. In the preceding code, you apply the style instructions inside the curly brackets associated with the <body> HTML tag. The text before the first curly bracket indicates which tag is formatted.

Within the block live a number of style definitions, with the name on the left (such as font-size) and the setting on the right (such as 12px). Each line ends with a semi-colon (;). The CSS specification published by the World Wide Web Consortium (W3C) provides a range of style definitions that you can use to format your HTML.

The first step is to set the font characteristics. The first instruction (font-family) describes the font to be used. You should specify three fonts separated by commas in order of preference. If a font name includes a space, put the font name in quotes (such as "trebuchet ms"). It is also advisable to always use sans-serif as the third font option because all computers come with a sans-serif typeface. Next, font-size (rather unsurprisingly) specifies the font size. The size is specified in pixels by using px. As such, 12px refers to a font 12 pixels in size.

CSS provides a lot of different methods for setting sizes. Table A-1 shows the common types.

# TABLE A-1  The Major Measurement Types Are All Relative to Something Else

| MEASUREMENT | DESCRIPTION |
| :--- | :--- |
| Px | This is the pixel size, relative to the size of the resolution of the page. |
| Em | This size is relative to the height of the font. |
| Ex | This size, used infrequently, is relative to the size of the letter X. |

The next element (line-height) determines the distance between lines of text. The value here is specified in em, which sets the size relative to the font size set earlier.

The next two elements (color and background) specify the color of the font (color) and the color of the background of the page (background).

The next two attributes (margin and padding) specify the space around an object (margin) or space around the content inside an object (padding). Finally, text-align indicates how the text is justified, and width simply specifies the width as a percentage. Setting the width value to 100% displays the item at the full width of the page.