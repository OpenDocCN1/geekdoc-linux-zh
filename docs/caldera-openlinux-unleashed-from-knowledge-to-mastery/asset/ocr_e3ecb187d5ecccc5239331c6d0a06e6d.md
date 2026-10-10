All the information necessary to develop this typeset document is contained in the control information provided by TeX information lines beginning with \ and in the document class definition invoked by the `\documentclass{article}` line in Listing 28.1.

Well that was easy, wasn’t it? Unfortunately, the devil is in the details, and there are a lot of details.

# # Typesetting Entry Tools

Many tools are available for Linux that make the entry of typeset material easier: emacs (which is on the Caldera distribution CD) is a favorite of many UNIX enthusiasts, but LyX, which will assist you in inserting images and graphics into the finished document, is probably a better choice for the other 90 percent of us. Because an excellent version of LyX is included on the Caldera distribution CD, I will concentrate on it here.

# ## Creating a LaTeX Input File

You can create a LaTeX input file using virtually any text processing program. When you become familiar with Caldera OpenLinux, you will probably want to use emacs; but vi, Star Office, and WordPerfect are all acceptable.

The best option, one with a beautiful font end for LaTeX, is LyX (the Caldera distribution version is called KLyX). It combines the comfortable usage of a word processor with the high quality of LaTeX's typesetting, providing an almost WYSIWYG view of the document. Although line and page breaks aren't displayed exactly as they will be in the printed document, most everything else is.

LyX frees you from dealing with low-level formatting such as Large Bold Italic Sans Serif Font and a Little Space Above and Below and allows you to concentrate on the content. The typesetter (that is, LaTeX) has enough information to break your text in a very nice manner, so let it. You can simply choose a layout for each paragraph and leave the driving to the system.

This produces portable documents using a generic mark-up concept. Of course, you can still do low-level formatting, but the usual way is to tell LyX what the text is, not what it should look like. In a sense, LyX gives you WYSIWYM (What You See Is What You Mean) editing.

The LyX organization's Web page can be found at http://www.lyx.org. It contains a number of insights and other helpful information on LyX, as well as hints and current versions of the product.

Caldera's implementation of LyX that is delivered with Caldera is called KLyX. It can be found on the desktop options bar under the K-gear icon, Applications, KLyX, or it can be entered from a terminal running under X with the following command: