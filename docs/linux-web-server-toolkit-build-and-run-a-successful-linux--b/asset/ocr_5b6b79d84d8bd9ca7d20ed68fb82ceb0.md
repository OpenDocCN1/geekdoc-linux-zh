# Chapter 19: Maintaining Your Web Pages 439

such as WordPerfect. For example, ispell will suggest that some words should be hyphenated, or it may suggest plural alternates for words that aren't recognized. But with a few minutes of practice and your fingers on the right keys, spell checking in ispell can be much quicker in a word processor.

You will need to manually skip over HTML tags in ispell, however, which can slow down checking in Web pages. If you have a lot of Web pages to check and they were created with a tool that doesn't allow spell checking while skipping HTML tags, the quickest route may be to save the pages as plaintext in your browser (this removes all HTML tags), and then use ispell to check them for typos or other spelling errors. If you find any, go back to the original HTML documents and search for the error to correct it.

# Using HTML Validation Tools

A fairly recent development among Web authorizing programs, HTML validation tools allow you to check the accuracy of many facets of your Web pages against standardized HTML. This type of check can provide many benefits,:

+   Consistent look among all the pages on your Web site (slight variations in how HTML tags are coded change the way Web pages look; bullet lists, graphics, and other elements can appear differently if HTML tags are not consistent).

+   Elimination of errors across a variety of browsers (different methods of displaying nonstandard HTML or may disregard completely HTML tags that don't match a known template).

+   Track and update information on your Web site with automated tools (because of consistency in tags, automated programs can find exactly what they need to update).

![](bbox=[0.047, 0.735, 0.819, 0.893])

The best way to produce error-free HTML pages is to generate them automatically instead of having a person write them. Anytime you want to deliver information on the Web that is already in electronic format (such as database records, catalog listings, or poetry collections in a word processor) you can write a script to convert the material to HTML. The script can create HTML-on-the-fly as pages are requested or in advance as you develop your site content. The key is to test the script to see that it produces correct HTML.