which can then be adapted to your needs. Figure 11-10 shows the form for creat-\ing both pages.

Save time, create the search interface pages after you have defined all the metadata and
indexes in your catalog, because these will be used to create search and results pages. If
y add metadata or indexes later, you will need to modify the pages manually.

Figure 11-10 shows the form used to create a Z Search Interface. Following
the figure is an explanation of the fields on this form.

![](bbox=[0.189, 0.209, 0.814, 0.366])

Figure 11-10: Farm for creating a search and results page

Select one or more searchable objects:
This list contains all searchable objects (ZCatalog, Z SQL methods) that can be
acquired from the current folder (that is, those in the folder's namespace stack).
You can select one or more searchable objects from this list.

Report Id and Report Title:
These are the id and title of the search page to be created.

Report Style:
This offers two options for presenting the results of the search: in tables or as
records. The former displays each object found on a row of a table, with each
metadata element in its own column. The latter displays the metadata of each
object on a line separated by commas.

Search Input Id and Search Input Title:
Use these fields to specify the id and title for the search page, which is a form for
users to provide the criteria with to search the ZCatalog.

# 11.3.1 The Search Page

The search page consists of a simple HTML form arranged in a table, as shown in
Listing 11-1. The individual cells in the table are automatically created when you
create the search page, according to the objects to be searched using this form.