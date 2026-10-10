![](bbox=[0.05, 0.08, 0.69, 0.42])

scoring itself. Just check one of the boxes next to “word” or “line” and save your change with the State menu.

When adaptive scoring is turned on, Gnus begins to notice which articles you delete unread, which you save, and the sort of threads that interest you. It accumulates this information throughout a news-reading session, and when you quit, it neatly deposits the information in one or more score files. It takes a while for Gnus to build up enough information in the score files to make a noticeable difference, but after a week of daily news reading, your Summary buffers will display interesting posts prominently, while the annoying stuff begins to recede into the background. Think of scoring as a form of self-defense.

# The Local Cache

In Gnus terminology, a cache is a directory tree where articles can be stored, either temporarily (until you have time to read them) or permanently. You can use the cache (which is a subdirectory of your ~/News directory) as an alternative means of saving a local copy of an article. The cache can also speed up subsequent Gnus sessions, because Gnus will load an article from the cache instead of downloading it from the server if it has a choice. Here are a few of the commands that copy articles to the cache: