object, the higher up in the list the object be.
Text indexes also support simple boolean expressions (using "and," "or," or "and not") and partial word matching using "?" matches any single character and "*" matches any substring of characters. To use wildcards, the ZCatalog's vocabulary must have globbing support enabled (see Section 11.1.2 for details). Built-in automatic support matches multiple word forms, so that a search for the word "walk" will also match "walks" and "walking" in the cataloged object.

Text indexes are used on text or string attributes that will contain multiple words or long passages of text. They can also be useful for single-word values if wildcard and multiple-word form matching is important.

![](bbox=[0.273, 0.068, 0.303, 0.142])

When text is indexed in a text index, all punctuation, capitalization, and numeric data text are ignored.

# 11.5.2 Field index

A field index is a simple index that searches against the entire value of an attribute value. With a field index, you can find objects by exactly matching the indexed value or by specifying a range that it must fall (see section 11.4.3.2 for more on range searching). Field indexes are ideal for indexing numeric or date/time data. They are also useful for indexing short string values that should be matched exactly, such as an object's meta_type attribute.

# 11.5.3 Keyword index

A keyword index allows you to search for a list of values, such as lines or tokens property. To match a keyword index, you must match only one element of the indexed value list.

As its names, keyword indexes are useful for keyword searches. They are also useful as a way to express one-to-many relationships between objects. For example, you can use a lines property in an object to store the ids of related objects, create an index on the property and use it to find objects related to one another.

# 11.2.6 Advanced Screen

The advanced screen is divided into two sections: Catalog Maintenance and Subtransactions, as shown in Figure 11-9.

# 11.2.6.1 Catalog Maintenance

Two buttons appear in the top section of the Advanced ZCatalog screen: Update Catalog and Clear Catalog.

Update Catalog reindexes all objects that are currently indexed in the ZCatalog updates the metadata table. It also removes the entries for any indexed objects that have been deleted but not removed from the catalog. Use it when you have added new indexes or metadata elements to your catalog to populate their values from the objects in the catalog.

The Clear Catalog button removes all cataloged objects from the ZCatalog. After using it, you can use the Find Objects tab to repopulate the ZCatalog.