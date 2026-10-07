# Table 7-8 Statistics from the memstat Command (Continued)

| Counter | Description |
|---|---|
| fpi | Regular file page-ins — The number of pages from regular files paged since the last sample. A file page-in occurs whenever a page for a regular file is read in from the file system (part of the normal file system read process). |
| fpo | The number of regular file pages that were paged out and freed, usually as a result of being paged out by the page scanner or by write free-behind (when free memory is less than `lotsfree + pages_before_pager`). |
| fpf | Regular file page-frees — The number of regular file pages that were freed, usually as a result of being paged out by the page scanner or by write free-behind (when free memory is less than `lotsfree + pages_before_pager`). |