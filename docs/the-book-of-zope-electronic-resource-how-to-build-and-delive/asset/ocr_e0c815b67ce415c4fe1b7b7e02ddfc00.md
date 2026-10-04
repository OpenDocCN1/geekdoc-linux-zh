# Search only in this folder and Search all subfolders

Check one option to search for objects in a specific folder selected with the Find tab. Select only this folder to search through the current folder; Select all subfolders to search the entire Zope structure from the current folder down. Search the entire Zope server, open the root folder and perform your search from there, choosing the Search all subfolders option.

# Find

For example, here's how you search for all DTML methods and documents that use the standard HTML header and that were edited after February 4, 2000:

+   1. Change to the root folder and click the Find tab.
2. Select DTML method and DTML document.
3. In the modified field, enter the date 2000/02/04.
4. In the containing field, enter `<dtml-var standard_html_header>`.
5. Leave Search all subfolders selected.
6. Click Find.

In response, the top of the screen should display links to all objects that match the search criteria, as shown in Figure 3-9, which shows 12 found objects. Clicking one of these links opens the object so that you can edit it.

| Contents | View | Properties | Security | Undo | Ownership | Find |
|---|---|---|---|---|---|---|n| Folder at / | Help |
| Displaying 1-12 of 12 items matching your query. You can revise your search terms below. | |
| Folder1/document1 (first DTML document) | |
| Folder1/Subfolder1/document2 | |
| Folder1/document2 | |
| Folder1/index/index_html | |
| MyHomepage/index/index_html | |
| index_html | |
| Folder1/method1 (my first DTML method) | |
| Folder1/Subfolder1/method2 | |
| Folder1/method2 | |
| Folder1/Subfolder1/method3 | |
| Folder1/method3 | |
| standard_error_message (Standard Error Message) | |

Figure 3-9: This example shows that twelve objects were found, each of which can be accessed using the links.