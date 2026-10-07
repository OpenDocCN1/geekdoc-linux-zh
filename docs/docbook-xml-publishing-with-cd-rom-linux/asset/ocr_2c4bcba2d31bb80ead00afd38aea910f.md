# Chapter 4: Preparing a Book with DocBook

![](bbox=[0.169, 0.066, 0.804, 0.461])

4.3 The XML declaration in Emacs

# The BookInfo Element

There is some other information you will probably want to include about the book, things such as the title of the book, the name of the author or authors, the copyright holder, and other meta information about the book itself. To do that, you start with the BookInfo element.

You will look at two examples of the BookInfo element, a simple one and a more complex example that illustrates the range of information you can include within the BookInfo element.

The first example is for a book with only one author and includes a copyright holder and the year of the copyright (see Figure 4.4):

```
<book>
<bookinfo>
<title>DocBook Publishing</title>
<author>
  <firstname>Joe</firstname>
```