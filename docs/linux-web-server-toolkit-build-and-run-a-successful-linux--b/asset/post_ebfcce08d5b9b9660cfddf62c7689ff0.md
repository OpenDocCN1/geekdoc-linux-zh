
grammar errors that need the human touch to be caught and corrected for a top-quality Web page.

> Webster's a comprehensive online spell checker for Web documents. Just go to their site http://www.goldendome.net/Tools/Webster/ and submit your URL.

## ispell

If you prefer to use a command line tool in Linux to check spelling, you can try the ispell program, which is shown checking a document in Figure 19-1.

![](img/e01f1106dd2902613fa07890c8baa7e6_465_0.png)

Figure 19-1: The ispell program provides a very fast spell checking system for text documents.

The ispell program is a very basic spell checker. It includes features like personal dictionaries, and it can process very large documents quickly (depending on how many words it stops on). To start ispell, just run the program from a command line with the name of the file to spell-check:

- $ document.txt

You need to watch carefully when you use ispell, however, because the suggestions it makes are usually different from what you'll see in standard word processors, such as WordPerfect. For example, ispell will suggest that some words should be hyphenated, or it may suggest plural alternates for words that aren't recognized. But with a few minutes of practice and your fingers on the right keys, spell checking in ispell can be much quicker in a word processor.

You will need to manually skip over HTML tags in ispell, however, which can slow down checking in Web pages. If you have a lot of Web pages to check and they were created with a tool that doesn't allow spell checking while skipping HTML tags, the quickest route may be to save the pages as plaintext in your browser (this removes all HTML tags), and then use ispell to check them for typos or other spelling errors. If you find any, go back to the original HTML documents and search for the error to correct it.

## Using HTML Validation Tools

A fairly recent development among Web authorizing programs, HTML validation tools allow you to check the accuracy of many facets of your Web pages against standardized HTML. This type of check can provide many benefits:

- Consistent look among all the pages on your Web site (slight variations in how HTML tags are coded change the way Web pages look; bullet lists, graphics, and other elements can appear differently if HTML tags are not consistent).

- Elimination of errors across a variety of browsers (different methods of displaying nonstandard HTML or may disregard completely HTML tags that don't match a known template).

- Track and update information on your Web site with automated tools (because of consistency in tags, automated programs can find exactly what they need to update).

![](img/e01f1106dd2902613fa07890c8baa7e6_466_0.png)

The best way to produce error-free HTML pages is to generate them automatically instead of having a person write them. Anytime you want to deliver information on the Web that is already in electronic format (such as database records, catalog listings, or poetry collections in a word processor) you can write a script to convert the material to HTML. The script can create HTML-on-the-fly as pages are requested or in advance as you develop your site content. The key is to test the script to see that it produces correct HTML.

## Linux Web Server Toolkit

Some of the errors that are the easiest things for a validation program to find are the hardest for a person to spot. Computers love tedium. For example, if you miss a glaring quotation mark on a URL in an <IMG> or <A> tag, the rest of the document may not work. If you don't end a bulleted list with a </URL> tag, the rest of the document will be indented. And if you miss a cell in a table that you create, everything in the table will be incorrectly aligned.

These examples may be prevented if you're using some HTML generation programs, and most would be noticed by the review team during the review process. Other problems won't be noticed until someone with a different type of browser tries to read your page and can't, or until someone in another domain tries to follow one of your relative links and can't.

## Finding the Right HTML Validation Tools

Different types of HTML tools perform different types of inspections. You should review the list of checks that a tool performs when deciding on a tool or set of tools.

Many of the HTML validation "tools" are actually services. A Web page validation allows you to submit a page for review and will return a report on that page fared. Figure 19-2 shows a submission form for the WebTechs HTML Validation Service (http://www.webtechs.com/html-val-sec/).

![](img/e01f1106dd2902613fa07890c8baa7e6_467_0.png)

Figure 19-2: Using an HTML validation service like WebTechs, you can submit your URL and the type of analysis you performed and let your automated tools check your page for many facets of correctness.

This section lists only free tools; however, there are many commercial HTML validation tools available. You can find a list of tools by looking on the Yahoo site (http://www.yahoo.com/) under Computers, WWW, HTML. New HTML validation tools seem to appear every week. Some of the most popular ones are listed in Table 19-2.

## Table 19-2 HTML Validation Tools

| Tool | Description | URL |
| --- | --- | --- |
| Doctor HTML | A complete Web page examination tool that does spell checking of HTML pages, hyperlink verification, and syntax tests on your HTML tags. | http://imagiware.com/RxHTML.cgi |
| WebTechs HTML Validation Service | Verifies your page conforms to the Internet Engineering Task Force standards for HTML. It can also determine how well suited your page is for different types of browsers. | http://www.webtechs.com/html-val-svc |
| Dr. Watson | An HTML validation service with spell checking, link verification, and syntax analysis. | http://www.addy.com/watson/ |
| Htmlcheck | Checks your HTML page for a number of syntactic errors. | http://uts.cc.utexas.edu/~church/htmlcheck.html |
| Meta Medic | Tests the content of your meta tags (tags in the HEAD section of your document that provide information about the document but are not displayed) for compatibility with popular search engines that review these tags. | http://www.northernwebs.com/set/.html |
| NetMechanic | An online service that reviews your site for bad HTML tags, missing links, and server response time. | http://www.netmechanic.com |
| Missinglink | A shareware program that runs on the server to check the validity of links. | http://www.rsol.com/ml/ |
| Webxref | A Perl program for your server provides easy and quick cross referencing of your complete set of documents. | http://www.sara.nl/cgi-bin/rick_acc_webxref |

## Linux Web Server Toolkit

Some Web sites provide an HTML validation button at the bottom of their pages. When the button is clicked, an HTML validation program is run on that page. Figure 19-3 shows an HTML validation button that uses the WebTechs service. You can download the button from WebTechs site (see http://www.webtechs.com) and add it to any of your pages. While this might seem a strange way to involve your visitors in your development, it serves several purposes.

![](img/e01f1106dd2902613fa07890c8baa7e6_469_0.png)

19-3: A button like the one on the left at bottom of the page allows users to check the page's HTML code for errors.

It provides an additional check on your pages, so that users can report errors that were missed by your own reviews. It also shows them their interest in maintaining correctness and up-to-date pages.

Perhaps the best reason to include a validation button this is: A user who is convinced that a problem exists because of an error in your HTML coding can run a validation check to find out that the problem is actually caused by their own browser.

## A Good Link Checker (and it's Free)

I also want to mention a free tool, called HTML Analyzer and written in C, that can be used to produce a report of broken links and inconsistent usage of links on your pages. It produces a nice database of results.
