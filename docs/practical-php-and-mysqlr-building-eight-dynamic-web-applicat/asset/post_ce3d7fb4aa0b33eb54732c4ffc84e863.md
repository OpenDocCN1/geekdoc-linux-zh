
The first number next to the LIMIT keyword determines where the page begins, and this changes depending on the current page number (indicated by $validpage). This calculation is simple:

```php
echo "<p>";
$offset = ($validpage - 1) * $pagesize;
```

Here you simply subtract 1 from $validpage because the LIMIT keyword begins at 0 and not 1. Then you multiply the value by the page size. This indicated the correct range.

Gather the results for this range:

```php
$offset = ($validpage - 1) * $pagesize;
$pagersql = $query . " ORDER BY dateposted DESC LIMIT " . $offset . ", " . $pagesize . ";";
$pageres = mysql_query($pagersql);
$pagenumrows = mysql_num_rows($pageres);
```

```php
while($pagerow = mysql_fetch_assoc($pageres)) {
    echo "<h2><a href='viewstory.php?id=" . $pagerow['id'] . ">"
        . $pagerow['subject'] . "</a></h2>";
    echo "Posted on " . date('D jS F Y',
        strtotime($pagerow['date']));
    short_description($pagerow['body']);
}
```

Here you construct the query and add the LIMIT section with the offset. The results are then displayed, using short_description() to show the shortened story description.

To make the different pages easy to navigate, provide a series of links that users can click to choose the page they want:

```php
short_description($pagerow['body']);
}

echo "<p>";
echo "<strong>Pages: </strong>";

for($i=1; $i <= $numpages; $i++) {
    if($i == $validpage) {
        echo "<strong>&bull;" . $i . "&bull;</strong> ";
    }
    else {
        echo "<a href='search.php?term=" . $_GET['term'] . "&page=" . $i
            . "'>" . $i . "</a>" . ",";
    }
}
```

This code uses a for loop to loop between 1 and the value of $numpages and to display the number. A check is made to see if the current number in the loop is equal to the current page (stored in $validpage). If so, the number is displayed in bold without a link. Any other number is displayed as a link to search.php with the page GET variable added.

Finally, include the footer file:

```php
}
}
require("footer.php");
?>
```

![](img/c75d0c4fa51711b62f211459ae794f3f_481_0.png)

> **For Those About to Hit the Big Time...**
> 
> Remember that when you have a lot more stories, you can change the $pagesize variable to a larger page size—the script adjusts automatically.

# SUMMARY

In this project, you have rattled down a familiar road, but cemented many of the concepts and techniques explored previously in the book. In addition, you rolled in some new skills by using HTML_QuickForm. The assumption is that this project has been more of a breeze than previous ones. If you found it a piece of cake, rest assured that PHP is solidifying nicely in your head. Before long you will be creating your own awesome sites.

Well, this is the last project in the book. If you started at the beginning and worked through each chapter in turn, you have been on a long and expansive journey through PHP and MySQL application development. You have learned a variety of techniques, refined key skills, learned about the opportunities and risks that the Web offers, and so much more. All in all, you have had a solid grounding in PHP and MySQL development.

Although this is all nice and warm and fuzzy, the real challenge begins now. You essentially have two options after you put this book down. On one hand, you can feel content that you “learned PHP and MySQL” and not return to the book or write any new code. This is a bad idea. Knowledge only cements in the brain if it is used and reused and tested in different scenarios and contexts. The better option is to keep writing more code, keep improving the applications, and keep the cogs of PHP and MySQL turning. There are hundreds of potential ideas and applications you could write with the knowledge that you have just learned and invested in. Now is the time to make use of it—it will not only result in cool new applications, but it will make you a better developer. If you are stuck for things to code, why not contribute to one of the hundreds of open-source PHP and MySQL applications out there?

Good luck, and I wish you all the best for your future development!

# APPENDIX A

# Web Site Design

Design is a complex science, particularly if you lack any artistic talent. For many, the challenge of creating a visually appealing Web site is one marred with the uncomfortable feeling that despite your best efforts, the resulting design will look ugly, blocky, and predictable.

Although those who lack artistic chops are unlikely to give leading Web designers a run for their money, there is still a lot you can achieve by following some basic design principles. Many of the most popular and usable sites on the Internet have clean and effective designs driven by a series of simple yet powerful design decisions.

In this chapter, you will explore how to build some attractive and usable designs. These designs provide simple and consistent site layouts that your visitors will find usable. Good usability is, after all, the big win in good design.

## PROJECT OVERVIEW

In ye old days of the Web, design was really secondary to content. The majority of Web sites looked plain and simple. Most design was performed using the limited set of HTML tags available in the early days of the Web.

As the Web grew larger and sites had more and more pages, the challenge of managing a consistent design became apparent. When a fresh design was created for a site, the task of the unlucky Web developer was to go through each and every page on the site and apply the new design changes. For sites with hundreds of Web pages, this was a mundane and error-prone task. Since those dim and distant days, Cascading Style Sheets (CSS) has burst onto the scene and dramatically eased how design is handled.

CSS allows you to centralize the design in your Web site. Instead of applying the design via HTML tags, you create a special style sheet file that is loaded by each page on the site. With CSS, you can dramatically change the design of the entire site by changing a single file.

In this project, you will create and style a simple home page. The project covers a range of common design requirements, including general page design, and styling lists, headings, and tables. The stylesheet that you create in this chapter will be the basis for the rest of the projects in the book, as well, showing you how CSS can be applied not only across several pages, but also across entire Web applications.

To demonstrate how CSS can drastically change a page’s design, take a look at the simple page shown in Figure A-1. The page is rather dull, uninteresting, and plain.

![](img/c75d0c4fa51711b62f211459ae794f3f_484_0.png)

FIGURE A-1 Pages that don’t use CSS (or some other means of style) look boring.

When you link the stylesheet that is developed in this chapter, you get the more interesting page shown in Figure A-2.

![](img/c75d0c4fa51711b62f211459ae794f3f_485_0.png)

FIGURE A-2 A little CSS makes a world of difference; the simple page suddenly looks clean and organized, instead of bland and clunky.

A key goal when designing with CSS is that you should not need to touch the HTML code. The aim of CSS is that you can change the entire design of a site by changing a single stylesheet, making design both simple and scalable throughout the site.

> TIP In addition to good CSS design, you’ll have to resist the urge to add “just a little bit” of style in your HTML—leave those font and align tags and attributes behind.

# LAYING OUT THE SITE

When you create a CSS-driven design, you use HTML to specify the purpose of different parts of the page. At the top of the page, for example, you may want an area that contains the name of the site. To outline this area, you use the HTML <div> tag to identify it.
