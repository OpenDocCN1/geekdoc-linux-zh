# # GET PRODUCTIVE

# ## LibreOffice Templates

![](bbox=[0.08, 0.09, 0.63, 0.42])

paths listed in `Tools | Options | Paths`. By default, that means the templates in your home directory, although the path might also include a template repository available to all users on the system.

Across the top of the Template Manager are three ways of locating registered templates: a search field, a LibreOffice module filter, and a category filter. The bottom of the window are tools for managing the view of the editing window and for importing and exporting files. To work with a particular template, right-click on it. From the right-click menu, you can start a new document based on the selected template, set the selected template as the default for its LibreOffice Module, or open the template to edit. If you are editing, you can use the regular `File | Save` dialog, since the template is already registered.

You cannot delete templates installed with LibreOffice through an extension or for the entire system, although you can delete the extension from `Tools | Extension Manager`. However, templates made from the editing window can be deleted – but be careful, because the Template Manager does not include confirmation dialogs. From within the Template Manager, select the template to delete, and then click the Delete button.

# ### CIRCUMVENTING TEMPLATE LIMITATIONS

For years, Microsoft Word was notorious for allowing more than one template to be applied to a document. "Too often, the result was unrecoverable file corruption. When StarOffice, LibreOffice’s first ancestor, was written, mixing templates was made impossible to avoid such problems. The only trouble is, users still need a convenient way to alter templates and the files associated with them.

The most convenient way to alter a template and the documents based on it is to edit the template by right-clicking on it in the Template Manager. After you have saved the revised template, the next time you open an associated file, you are given the opportunity to upgrade it (Figure 4). If you upgrade, the association between the template and the document continues, and further changes to the template will trigger the upgrade dialog. However, if you do not upgrade the document, its link with the template is severed – although, somewhat confusedly, the template continues to be listed in `File | Properties | General`. You sometimes find an extension that is supposed to allow you to change templates, but, like all extensions, you use such tools at your own risk. Considering the problems that have existed in Microsoft Word for decades, you are probably safest avoiding such tools.

One way to reattach a document to a template is to open a new document using the template and then copy and paste the unattached file into it. Be careful, though, to Use Paste and not Paste Special. In some circumstances, a possible solution may be to design a new template, carefully using the same style names, and then overwrite the original template name. The new template will be treated as a revision of the original, so associated files can be updated when each one is opened.

A temporary solution is to use a Master Document. In the past, Master Documents were used to divide long files into divisions small enough to work with limited memory. Today, they are still used to allow more than one person to simultaneously work on a document. However, what matters here is that a Master Document can use a different template than any of its component files – even if only one file is involved. To take advantage of this feature, start a new document using the revised template and then select `File | Send | Master Document`. Then open the Master Document. From the right-click menu, select `Insert | File` to add the document from the file manager, and select `Update | All` to apply the Master Document’s formatting to it. Close the Master Document without saving, and you will still be able to open the document in its original format. Should you decide to keep the Master Document’s format, select `Edit` from the right-click menu to open the document in an editing window, from which you can save it using the Master Document’s template.

![](bbox=[0.36, 0.87, 0.92, 0.95])