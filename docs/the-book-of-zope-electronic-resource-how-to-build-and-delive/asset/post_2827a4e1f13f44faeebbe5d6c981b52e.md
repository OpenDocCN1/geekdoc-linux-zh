
# Listing 11-2: Code for queryForm DTML document

```
<dtml-var standard_html_header>
<form action="queryReport">
<p>Title:<input type="text" name="title" size="40"></p>
<input type="submit">
</form>

<dtml-var standard_html_footer>
```

Listing 11-3 shows the code for queryReport, which lists the titles of the cataloged objects found, based on the title entry made in queryForm.

# Listing 11-3: Code for queryReport DTML Document

```
<dtml-var standard_html_header>
<dtml-in name="Catalog">
<dtml-var name="title"><br>
</dtml-in>
<dtml-var standard_html_footer>
```

The most important line of code in queryReport is the dtml-in statement on the second line. This statement calls the Catalog by name, passing it any values submitted from the form. If the user types words into the title field of the form and submits it, these words are used as search criteria against the title index in the Catalog.

## 11.4.2 Catalog Brains

When a ZCatalog is called, as in our simple example queryForm, it does not return the actual objects matched by the query criteria. Instead it creates a sequence of brain objects that contain the cached metadata values of the matched objects along with several methods that can be put to various uses. It is very important to understand that when you are working with Catalog results, you are not working with the actual objects found, only their metadata. You can, however, explicitly access the actual objects if you need to.

Table 11-1 lists the methods available on the brain objects (that is, result items) returned from a ZCatalog. Each of these methods is directly available inside a dtml loop that iterates over the ZCatalog results (such as in queryForm above), because dtml-in puts each result item at the top of the name-space as it steps through the result sequence.

The most useful methods listed in Table 11-1 are getURL and getObject. The former can be used to easily create links in your results page to each object; the latter to access any additional object attributes—such as properties and methods—that you may need in addition to the metadata cached in the ZCatalog.

Calling getObject on many result objects can slow down your ZCatalog searches. Use it sparingly and with small batch sizes when using dtml-in.

# Table 11-1: ZCatalog Brain Methods

| ZCatalog Brain Method | Description |
| --- | --- |
| has_key(key) | Returns true if the result item has a metadata element named "key." |
| getPath() | Returns the physical path of the result item in your Zope hierarchy. |
| getURL() | Returns the absolute URL of the result item (which may differ from getPath()) if you are using virtual hosting. |
| getObject() | Returns the actual Zope object corresponding to the ZCatalog result. |
| getRID() | Returns the ZCatalog's internal record id for the result item, which is the same as the data_record_id_variable returned by ZCatalog. This can be used to uniquely identify results easily. |

Let's enhance our queryReport page (Listing 11-4) using the getURL method above, which will allow us to construct a link to each object returned by the query.

# Listing 11-4: Enhanced queryReport DTML document

```
<dtml-var standard_html_header>
<dtml-in name="Catalog">
  <a href="<dtml-var name="getURL">
    <dtml-var name="title">
  </a><br>
</dtml-in>
<dtml-var standard_html_footer>
```

By adding the anchor tag to the queryReport code and using the getURL method of the ZCatalog brain to insert the object's URL in the href attribute, each search result now links to the object found by the query.

## 11.4.3 Querying ZCatalogs Directly

To query a ZCatalog, we call the ZCatalog using an expression and explicitly pass the query criteria as arguments. The argument names match the indexes you wish to query against, and the values contain the query criteria for each named index. You can supply criteria for as few or as many indexes as you wish. (You can also use other arguments to control the sort order of the result items returned by the ZCatalog.)

Let's create some sample queries on a ZCatalog containing the indexes shown in Table 11-2 (which are the defaults created by Zope).

# Table 11-2: ZCatalog Indexes

| ZCatalog Indexes | Index Type |
| --- | --- |
| PrincipiaSearchSource | TextIndex |
| bobobase_modification_time | FieldIndex |
| id | FieldIndex |
| meta_type | FieldIndex |
| title | TextIndex |

### 11.4.3.1 Basic Field Index Queries

Field Indexes can be used to find objects whose attributes match the values you specify. To match objects with a field index, we simply pass arguments the name of each index we want to match, followed by the value desired. For example, to find all catalog objects with the meta_type value 'DTML Document' and the id value 'index_html', you would use the following ZCatalog query expression:

```
expr=Catalog(id='index_html', meta_type='DTML Document')
```

When you pass multiple indexes, they are 'anded' to form the search query, meaning that all criteria must be matched for the object to be returned in a result. To expand the search to match multiple values of an indexed attribute simultaneously, pass the desired values in a list to the index you are matching against. For example, to expand the above search to include DTML Document objects, use this expression:

```
expr=Catalog(id='index_html', meta_type={'DTML Document', 'DTML Method'})
```

When you use the above expression, a meta-type value of DTML Document or DTML Method, along with an id value of index_html, would satisfy the search criteria for an object.

> NOTE Keywords work the same way, except that the search value needs to match only one item of the keyword indexed list attribute (such as a lines or tokens property).

### 11.4.3.2 Range Queries on Field Indexes

It's a more complex process to match a field index against a range than it is to match it against an exact value. To match a range we must specify two arguments for the index, the desired range value(s) and range usage. The range value(s) are passed in an argument matching the name of the field index. The usage argument uses the field index name followed by _usage. The three usage values that control how the range matching is performed against the index are shown in Table 11-3.

# Table 11-3: Usage values for range matching

| Range usage value | Description |
| --- | --- |
| range:min | Matches indexed values equal to or greater than the range value. |
| range:max | Matches indexed values less than or equal to the range value. |
| range:min:max | Matches indexed values between a specified and maximum value. |

For example, let's consider how we query the ZCatalog by date, using the bobabase_modification_time index to find objects based on their modified date and time.

For our first example, let's find all cataloged objects modified in the last 30 days. This could be used in our bookstore application to find recently added or modified instances.

```
expr="Catalog(bobabase_modification_time=ZopeTime())-30,
bobabase_modification_time_usage='range:min'
```

In the first argument, which matches the index name, we pass the value of the current Zope date and time minus 30, which calculates the date 30 days prior to our search value. The second usage argument instructs the ZCatalog to return objects whose date is equal to or greater than the search value.

By simply changing the usage value, we could find all objects that have not been modified for 30 days, as follows:

```
expr="Catalog(bobabase_modification_time=ZopeTime())-30,
bobabase_modification_time_usage='range:max'
```

To match values that fall between two values (a minimum and maximum), you must pass a list containing at least two items as the search value. The item of the list with the smallest value is treated as the minimum search value and the item with the largest value as the maximum search value. For example, to find all cataloged objects modified yesterday, we could use the following expression:

(ZopeTime()-1) returns the date and time 24 hours ago as a Date Object. To determine the starting and ending time of the previous day for our use as minimum and maximum values, we use the earliest() and latestTime() method respectively of the DateTime object. These are passed in a two-item list as the search value. We then use the range:min:max usage value to instruct the ZCatalog to perform the bounded query.
