
## LibreOffice Templates

paths listed in `Tools | Options | Paths`. By default, that means the templates in your home directory, although the path might also include a template repository available to all users on the system.

Across the top of the Template Manager are three ways of locating registered templates: a search field, a LibreOffice module filter, and a category filter. The bottom of the window are tools for managing the view of the editing window and for importing and exporting files. To work with a particular template, right-click on it. From the right-click menu, you can start a new document based on the selected template, set the selected template as the default for its LibreOffice Module, or open the template to edit. If you are editing, you can use the regular `File | Save` dialog, since the template is already registered.

You cannot delete templates installed with LibreOffice through an extension or for the entire system, although you can delete the extension from `Tools | Extension Manager`. However, templates made from the editing window can be deleted – but be careful, because the Template Manager does not include confirmation dialogs. From within the Template Manager, select the template to delete, and then click the Delete button.

### CIRCUMVENTING TEMPLATE LIMITATIONS

For years, Microsoft Word was notorious for allowing more than one template to be applied to a document. "Too often, the result was unrecoverable file corruption. When StarOffice, LibreOffice’s first ancestor, was written, mixing templates was made impossible to avoid such problems. The only trouble is, users still need a convenient way to alter templates and the files associated with them.

The most convenient way to alter a template and the documents based on it is to edit the template by right-clicking on it in the Template Manager. After you have saved the revised template, the next time you open an associated file, you are given the opportunity to upgrade it (Figure 4). If you upgrade, the association between the template and the document continues, and further changes to the template will trigger the upgrade dialog. However, if you do not upgrade the document, its link with the template is severed – although, somewhat confusedly, the template continues to be listed in `File | Properties | General`. You sometimes find an extension that is supposed to allow you to change templates, but, like all extensions, you use such tools at your own risk. Considering the problems that have existed in Microsoft Word for decades, you are probably safest avoiding such tools.

One way to reattach a document to a template is to open a new document using the template and then copy and paste the unattached file into it. Be careful, though, to Use Paste and not Paste Special. In some circumstances, a possible solution may be to design a new template, carefully using the same style names, and then overwrite the original template name. The new template will be treated as a revision of the original, so associated files can be updated when each one is opened.

A temporary solution is to use a Master Document. In the past, Master Documents were used to divide long files into divisions small enough to work with limited memory. Today, they are still used to allow more than one person to simultaneously work on a document. However, what matters here is that a Master Document can use a different template than any of its component files – even if only one file is involved. To take advantage of this feature, start a new document using the revised template and then select `File | Send | Master Document`. Then open the Master Document. From the right-click menu, select `Insert | File` to add the document from the file manager, and select `Update | All` to apply the Master Document’s formatting to it. Close the Master Document without saving, and you will still be able to open the document in its original format. Should you decide to keep the Master Document’s format, select `Edit` from the right-click menu to open the document in an editing window, from which you can save it using the Master Document’s template.

![](img/e39350c3a7c0d527d71b0e4097a0ba66_57_1.png)

The idea of trusting your files to a Master Document may sound alarming if you are familiar with past versions of Microsoft Word, whose Master Documents were widely said to be in one of two conditions: corrupted and about to be corrupted. But while Master Documents are more robust, and, while they sometimes crash, they should not destroy their component files. Still, just to be safe, make sure that you have a current backup.

If you do not mind ignoring or losing the connection between a document and its template, you can partly reformat using *Edit | Paste Special | Unformatted Text* on a selection of text from another document. With this command, text in the original formatting is inserted using the formatting of the paragraph or character style in which it is placed. However, objects like images or tables are dropped and will have to be copied and pasted individually using *Edit | Paste*.

Similarly, you can import styles from another document using *Styles and Formatting | Load Styles*. This choice allows you to select both the files and the categories of styles to upload: *Text* (paragraph and characters), *Numbering*, *Frame*, and *Pages*. For fullest effect, use imported styles with the same names as those in the files and select the *Overwrite* box (Figure 5).

### BEST PRACTICES

Although you can circumvent the restrictions on templates if necessary, remember that the restrictions are designed to preserve your documents from harm. Generally, the following techniques should help you to use templates efficiently and without any difficulties:

- Avoid detaching documents from their templates whenever possible. Try not to detach the document unless it is only going to be used once, and its maintenance is unimportant.
- Change the formatting only on the template.
- Make all formatting changes on the template. Then apply the revised template to the document.
- Apply changes to a document as soon as they are made in the template. That way, you will not have to remember what changed, or wonder if you made an accidental change the next time that you open the document.

It can take several hours to design a template. Probably, you will want to make some tweaks after working with the template a time or two. However, once a template does what you want, it can save you hours and remain useful for years. Discipline yourself and work with the template system rather than opting for short-term convenience, and templates can be one of your most valuable tools in LibreOffice. ■■

![](img/e39350c3a7c0d527d71b0e4097a0ba66_58_0.png)

Figure 5: Loading styles from a template gives the effect of switching templates without actually doing so.

### INFO

- [1] **LibreOffice templates and extensions for downloading:** https://www.libreoffice.org/discover/templates-and-extensions/

## LibreOffice Macros

### Automating LibreOffice with macros

LibreOffice packs a built-in Basic-like scripting language that can be used to automate repetitive tasks and extend the suite’s default functionality. *By Dimitri Popov*

In skilled hands, the LibreOffice Basic scripting language can do wonders, but you don’t have to be a programming expert to write simple, or even more advanced, macros that perform useful tasks. Whether you are a Linux home user or an IT specialist, you can use the built-in scripting powers of the LibreOffice suite to automate recurring tasks. This article provides some examples you can use as building blocks for your own LibreOffice coding projects.

### LOOKING UP WORDS

The LibreOffice Basic macro editor is reachable through *Tools | Macros | Edit Macros* (Figure 1). Traditionally, an introduction to a programming language starts with a simple example that displays the “Hello world!” message. Although it’s cute, it’s not particularly useful, so instead, I’ll start with something more practical: a simple macro to look up the currently selected word in Wikipedia. The key element of the macro is the built-in *Shell1* function [1], which is used to call external programs. For example, you can use the following code to open the default browser on your machine:

```
Sub Main
Shell1 ("xdg-open", 1)
End Sub
```

The *Shell1* function requires the name of the program to run (you might need to add the path if the application is not in a location included in Bash’s *$PATH* environment variable). The second parameter is how you want the program to be opened (e.g., full-screen; minimized, maximized, or hidden program window; with and without focus, etc.).

For the record, *xdg-open* is the most common way to call the user’s preferred application for a given file type or URL. For example, running

```
xdg-open http://<some.url>
```

opens *http://<some.url>* in the user’s preferred web browser.

![](img/e39350c3a7c0d527d71b0e4097a0ba66_59_0.png)

Figure 1: The LibreOffice macro editor.
