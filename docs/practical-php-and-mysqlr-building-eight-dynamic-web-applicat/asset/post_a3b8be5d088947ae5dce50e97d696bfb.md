
`</div>`

`<div id="main">`

Create a file called `footer.php` and add the closing code (see Example A-2).

## EXAMPLE A-2  The footer file is very simple.

`</div>`

`</div>`

`</body>`

`</html>`

The footer code has the closing main and container `<div>` tags, as well as the closing `<body>` and `<html>` tags.

> **NOTE**
>
> **Wedging In Your Content**
>
> If you look at the bottom of the header file and the top of the footer file, you can see that the opening main `<div>` is at the end of the header file, and the closing main `<div>` is at the top of the footer file. If you now include the header.php file at the top of a script and include the footer.php at the bottom, all content in-between will appear in the main `<div>`. This is what you will do in all of the projects.

The next step is to add the code for the side bar. This side bar is included in the bar `<div>` in header.php. Create a new file called bar.php and add the following code (shown in Example A-3).

## EXAMPLE A-3  The side bar contains some simple information and a photo.

`<h1>Mug Shot</h1>`
`<img src="photo.jpg">`
`<h1>Details</h1>`
`<ul>`
`   <li>I am a workaholic</li>`
`   <li>I have two dogs called Banger and Frankie</li>`
`   <li>My favorite colour is blue</li>`
`</ul>`

This file references a photo of the owner of the site; therefore, you will need to create a 130×130 image and name it *photo.jpg*. Feel free to use any photo you like. You can also change the list items to match your own tastes and personal details.

## NOTE

### Unordered and Ordered Lists

In *bar.php*, you create an *unordered* list, and it displays as bullet points. You can also use an *ordered* list by using the `<ol>` tag (you still add `<li>` items inside the tag). An ordered list uses numbers instead of bullet points, such as:

- 1. One item.
- 2. Another item.
- 3. Guess what? Another item.
- 4. And one more.

Next, create the main page, or front page, for the site. Create a new file called *index.php* and add the following code shown in Example A-4.

**EXAMPLE A-4** The front page of the Web site contains a number of different HTML elements, but there is still no formatting; CSS will handle that task.

```php
<?php
require("header.php");
?>

<h1>Welcome!</h1>
<p>
Welcome to my website!
</p>
<p>
On this website, you can find a load of information about me
and the different things I am interested in. You can also find
out about my <i>superb</i> dogs and what they like to do.
</p>
<p>
On this website you can find out about:
<ul>
<li>My interests</li>
<li>My dogs</li>
<li>My website</li>
</ul>
</p>
<?php

require("footer.php");
?>
```

Inside this file you include a few paragraphs in `<p>` tags. If you want to create valid HTML, it is important that each paragraph is within both the opening `<p>` and closing `</p>` tags (just like with other tags such as `<i>` and `<strong>`).

> **NOTE**
>
> - `<b>` Versus `<strong>`
>
> As you wander the streets of the Internet learning about PHP and MySQL, you may see some people use the `<b>` tag instead of `<strong>` and wonder what the difference is. Surely they both just indicate bold text, right? Well, not so much.
>
> The `<strong>` tag is intended to add strong emphasis to the text it is applied to, whereas the `<b>` tag is intended to simply make text bold. This can cause an issue with some accessibility tools such as screen readers. If you want to ensure that your code works well on all browsers and devices, including accessibility software, use the `<strong>` tag.

# START BUILDING THE STYLESHEET

The main focus of this chapter is to cover how the CSS stylesheet is created. To make this as simple as possible, you will build up the stylesheet step by step.

To begin, create a new file called `stylesheet.css` and add the following block:

```css
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
```

Inside a stylesheet, a series of blocks apply style elements to different parts of the HTML. In the preceding code, you apply the style instructions inside the curly brackets associated with the `<body>` HTML tag. The text before the first curly bracket indicates which tag is formatted.

Within the block live a number of style definitions, with the name on the left (such as font-size) and the setting on the right (such as 12px). Each line ends with a semi-colon (;). The CSS specification published by the World Wide Web Consortium (W3C) provides a range of style definitions that you can use to format your HTML.

The first step is to set the font characteristics. The first instruction (font-family) describes the font to be used. You should specify three fonts separated by commas in order of preference. If a font name includes a space, put the font name in quotes (such as "trebuchet ms"). It is also advisable to always use sans-serif as the third font option because all computers come with a sans-serif typeface. Next, font-size (rather unsurprisingly) specifies the font size. The size is specified in pixels by using px. As such, 12px refers to a font 12 pixels in size.

CSS provides a lot of different methods for setting sizes. Table A-1 shows the common types.

## TABLE A-1  The Major Measurement Types Are All Relative to Something Else

| MEASUREMENT | DESCRIPTION |
| :--- | :--- |
| Px | This is the pixel size, relative to the size of the resolution of the page. |
| Em | This size is relative to the height of the font. |
| Ex | This size, used infrequently, is relative to the size of the letter X. |

The next element (line-height) determines the distance between lines of text. The value here is specified in em, which sets the size relative to the font size set earlier.

The next two elements (color and background) specify the color of the font (color) and the color of the background of the page (background).

The next two attributes (margin and padding) specify the space around an object (margin) or space around the content inside an object (padding). Finally, text-align indicates how the text is justified, and width simply specifies the width as a percentage. Setting the width value to 100% displays the item at the full width of the page.

> **NOTE**
>
> ### Colors in CSS and HTML
>
> Colors are referenced in hexadecimal, or hex, codes. Each code consists of a number of letters that range between 0 and F (0, 1, 2, 3, 4, 5, 6, 7, 8, 9, A, B, C, D, E, F). Each element ranges from the lowest value (0) to the highest value (F). Colors in HTML and CSS are usually expressed with a pound symbol (#) and six letters or numbers—for example, #FA34EE.
>
> The position of the letters indicates which color the letters refer to. The first two (#00__) are red, the second two (#__00__) are green, and the third two (#______) are blue. By combining the three color types and the variation between 0 and F, you can get a huge range of different colors.
>
> A shorthand method for specifying a code is also available with a single letter for each of the three colors—for example, #FFF.
>
> The majority of paint and photo retouching applications, as well as most Web editors, enable you to pick a color graphically and get the hex code.

> **NOTE**
>
> ### Browser Differences
>
> Some browsers deal with the margin and width properties in different ways. The main problem is with Internet Explorer, as it treats the measurements in margin and padding instructions differently. For details about these issues, see http://positioniseverything.net.

# FORMATTING THE MAIN <div> ITEMS

With the generic body section complete, you can move on to formatting each of the main `<div>` areas. As you format each `<div>`, you create formatting rules for the different tags inside it. For example, the `<h1>` tag should be formatted one way in the header section and differently in the side bar.

Aside from formatting the color, text, and other aspects of each `<div>`, you can also specify how each `<div>` is positioned on the page. You can use the static, absolute, relative, or fixed methods of positioning, with absolute and relative being the most common:

- Absolute: The position of the `<div>` is hard-coded to a specific area. With this type, you categorically state where the `<div>` is by providing coordinates.
