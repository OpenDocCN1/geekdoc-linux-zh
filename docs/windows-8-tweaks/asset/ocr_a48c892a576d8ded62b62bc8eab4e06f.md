service, Windows Search can quickly search through a file index that is con-tinuously updated by the indexing service running in the background. For a search in Windows to be successful, there needs to be a good balance between the amount of time it takes to get results and the overall system performance decrease caused by the background indexing service.

You can use some cool tricks to increase the success of a search while also increasing overall system performance by reducing the amount of work the index-ing service has to do. First, I show you how to adjust where Explorer searches for an item when browsing through folders. Then I show you how to adjust some settings on the indexing service, as well as how to use Windows Search without an index. All these hacks help you increase the performance of Windows Explorer and your overall system performance.

# ### Adjusting Search Settings

Typically when you use a search box when browsing through folders, you are looking for a specific file. In Windows, you can configure search to look for partial matches, the content of files, and within compressed files such as zip and cab files. By limiting what it is searching through, you can increase the speed with which your results are returned.

Adjusting the search settings is very easy to do. Follow these steps to adjust the search scope for any folder:

+   1. Open File Explorer.
2. Navigate to a folder for which you would like to change the search scope. Click the View tab and then click Options on the far right.
3. When Folder Options loads, click the Search tab.
5. Under How To Search, remove the check next to Find Partial Matches.
6. Under Searching Non-indexed Locations, you can configure whether you want to search system directories, within compressed files, and within the contents of files.
7. After you have made your changes, click OK to save them.

# ### Adjusting Windows Indexing Service

The search settings are just one part of the search feature in Windows. The real brains—the feature that enables you to search quickly through the various types of files on your computer—are in the indexing service. This service runs in the background and monitors only folders and file types it is configured to monitor. The content of any files located in folders the indexing service moni-tors are read by the service and indexed. That indexing data is then stored in a centralized database.