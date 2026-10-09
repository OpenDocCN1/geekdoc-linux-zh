# ## Searching Log Files

As you look through the various log files, you may soon realize that it is very difficult to keep track of failures and other alerts because of the large amount of information that is logged. For example, you may want to keep track of all login failures or certain hardware problems. How would you go about doing it? You can certainly schedule some time every day to wade through the entire content manually. However, this is far from efficient, and you could instead use your precious time for other system administration-related tasks. Or, you could use simple search tools to find specific information in the log files quickly and easily.

# ### Searching Log Files Using the System Logs Application

The System Logs application also provides a filtering option (you can see it at the bottom of the window in the screenshot below) – this allows you to search for specific words or phrases within a log file. For example, try selecting the System Log, typing the word fail into the Filter for textbox, and clicking the Filter button to execute the search. I found a few error messages:

![](bbox=[0.14, 0.36, 0.85, 0.8])

The application found seven entries from the System Log file that contained the word fail. In addition, it also highlighted entries where it found the word failed; you can configure what words trigger this effect by using the application's Edit | Preferences | Alerts option.