# **NOTE**
# Colors in CSS and HTML

Colors are referenced in hexadecimal, or hex, codes. Each code consists of a number of letters that range between 0 and F (0, 1, 2, 3, 4, 5, 6, 7, 8, 9, A, B, C, D, E, F). Each element ranges from the lowest value (0) to the highest value (F). Colors in HTML and CSS are usually expressed with a pound symbol (#) and six letters or numbers—for example, #FA34EE.

The position of the letters indicates which color the letters refer to. The first two (#00__) are red, the second two (#__00__) are green, and the third two (#______) are blue. By combining the three color types and the variation between 0 and F, you can get a huge range of different colors.

A shorthand method for specifying a code is also available with a single letter for each of the three colors—for example, #FFF.

The majority of paint and photo retouching applications, as well as most Web editors, enable you to pick a color graphically and get the hex code.

# **NOTE**
# Browser Differences

Some browsers deal with the margin and width properties in different ways. The main problem is with Internet Explorer, as it treats the measurements in margin and padding instructions differently. For details about these issues, see http://positioniseverything.net.

# # FORMATTING THE MAIN <div> ITEMS

With the generic body section complete, you can move on to formatting each of the main <div> areas. As you format each <div>, you create formatting rules for the different tags inside it. For example, the <h1> tag should be formatted one way in the header section and differently in the side bar.

Aside from formatting the color, text, and other aspects of each <div>, you can also specify how each <div> is positioned on the page. You can use the static, absolute, relative, or fixed methods of positioning, with absolute and relative being the most common:

+   • Absolute: The position of the <div> is hard-coded to a specific area. With this type, you categorically state where the <div> is by providing coordinates.