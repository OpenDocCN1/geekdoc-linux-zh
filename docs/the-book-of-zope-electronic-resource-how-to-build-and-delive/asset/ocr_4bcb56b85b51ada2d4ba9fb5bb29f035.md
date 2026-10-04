# Add ZCatalog

![](bbox=[0.226, 0.023, 0.814, 0.203])

As with all Zope objects, you must specify an id for the ZCatalog object; you may enter a title if you wish.

# 11.1.1 Choosing a Vocabulary

A vocabulary is a list of searchable words culled from objects cataloged in the ZCatalog. Objects are indexed in the ZCatalog using a TextIndex (see section 11.2.5.1), the text from the object is split into words and stored in the vocabulary in a manner that allows the catalog to quickly find which words are contained in which objects. When you create a ZCatalog, you may select an existing vocabulary or create a new one (see section 11.5, “The Vocabulary”). To do the latter, select the Create for me option to automatically create a vocabulary object inside your ZCatalog to store the word list.

This option allows you to share a vocabulary among several ZCatalogs—an important feature if you have several ZCatalogs that contain TextIndexes, because it is more efficient for them to share a single vocabulary than for each one. To share a vocabulary between ZCatalogs, create a vocabulary object (using the add menu) in a folder that's at or above the location of your ZCatalogs in the Zope hierarchy; then choose this vocabulary when you create each ZCatalog.

# 11.1.2 Globbing

If you create a vocabulary independently of a ZCatalog, you have the option to enable globbing, which allows you to use wildcard characters (such as asterisks (*) and question marks (?) in your ZCatalog searches to match partial words. Generally, you will want to enable globbing to give you greater search capabilities, but you can save memory and disk space by disabling it.

> Vocabularies created by ZCatalog automatically have globbing enabled.

# 11.2 The ZCatalog Screens

You are probably already familiar with several of the ZCatalog's tabs common to other objects (shown in Figure 11-2), including Content, Properties, View, Find, Security, Undo, and Ownership. But Figure 11-2 also shows five new tabs: Catalog, Indexes, Metadata, Find Objects, and Advanced—which will be explained in sections 11.2.2 through 11.2.6.