# ## CHAPTER

6

# # The Qt Namespace
and Qt Extensions

There are a couple of topics that bear discussing but are not so paper-consuming that they deserve an entire chapter. The first topic covered is the Qt class, which provides some commonly used enumerated constant values. The second topic discusses the Trolltech extensions to the Qt toolkit, which have evolved to a degree that the Trolls have moved the extensions out of the second release of the toolkit itself.

# ### QT CLASS

Providing global values is tacky and frowned on by almost every OO programmer. There are a lot of good reasons for this. The most compelling reason to avoid using global definitions is to avoid pollution of the development name space. The Microsoft development environment is a good example of a polluted environment—it is becoming increasingly difficult with every new release of VC++ to create a unique identifier name that doesn’t conflict with some macro in an included header file. As an example, consider the following macro definitions:

```
```c
...
#define AlignLeft      0x01
#define AlignRight     0x02
...
```
```