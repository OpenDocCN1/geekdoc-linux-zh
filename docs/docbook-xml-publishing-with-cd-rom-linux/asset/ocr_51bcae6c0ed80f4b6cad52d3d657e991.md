it is also valid to further describe the <sect1> element by using the label attribute, like this:

```
<sect1="1.1">
```

Using the label attribute can give the document more meaningful structure later when the document is processed and the section is identified as part 1.1 of the printed (or online) document. You do not have to choose a numeric label, however. You can just easily call that John if you want to, and the next three sections can be Paul, George, and Ringo.

More than likely, you will find that the DocBook set of elements is rich enough that it won't be necessary to make up elements; most possible cases have already been handled by existing elements. However, if you absolutely have to add an element for one reason or another, it can be done. Chapter 10, "Customizing DocBook," for more information on how to tailor DocBook to your specific needs.

I don't recommend adding elements to DocBook. However, there is a simplified DocBook DTD that contains a subset of the DocBook elements for those authors who don't want the entire set of DocBook elements. I cover the simplified DTD in Chapter 10, "Customizing DocBook."

Next you will see what an element looks like in a document and what each bit means.

# Anatomy of Markup Elements

If you haven't spent much time with HTML or a computer language, DocBook markup might look scary at first. It is, after all, designed to press a lot of information into a small space. Like any type of jargon, it is generally confusing to the uninitiated.

Each element is represented by a start tag and an end tag,

Here is an example of a normal element, with attributes:

```
<trademark class="registered">Linux</trademark>
```

The first part of the element, the start tag, begins with the < and is closed with the > symbol. The first word after the < is the element itself, and anything after that is an attribute of that element. In this case, class is the attribute, and registered is the value of the attribute. Some times the

![](bbox=[0.075, 0.455, 0.155, 0.56])