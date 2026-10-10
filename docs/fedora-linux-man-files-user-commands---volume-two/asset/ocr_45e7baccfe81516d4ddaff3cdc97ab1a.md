# NOTES

git-filter-branch allows you to make complex shell-scripted rewrites of your Git history, but you probably don’t need this flexibility if you’re simply *removing unwanted data* like large files or passwords. For those operations you may want to consider **The BFG Repo-Cleaner**[^1], a JVM-based alternative to git-filter-branch, typically at least 10-50x faster for those use-cases, and with quite different characteristics:

Any particular version of a file is cleaned exactly *once*. The BFG, unlike git-filter-branch, does not give you the opportunity to handle a file differently based on where or when it was committed within your history. This constraint gives the core performance benefit of The BFG, and is well-suited to the task of cleansing bad data - you don’t care *where* the bad data is, you just want it *gone*.

By default The BFG takes full advantage of multi-core machines, cleansing commit file-trees in parallel. git-filter-branch cleans commits sequentially (i.e. in a single-threaded manner), though it is possible to write filters that include their own parallelism, in the scripts executed against each commit.

The **command options**[^1] are much more restrictive than git-filter-branch, and dedicated just to the tasks of removing unwanted data- e.g.:—strip-blobs-bigger-than 1M.