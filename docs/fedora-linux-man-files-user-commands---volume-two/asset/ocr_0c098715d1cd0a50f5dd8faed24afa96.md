# TEMPORARY FILES

git mergetool creates `*.orig` backup files while resolving merges. These are safe to remove once a file has been merged and its git mergetool session has completed. Setting the `mergetool.keepBackup` configuration variable to `false` causes git mergetool to automatically remove the backup as files are successfully merged.