280 Chapter 15 Shell Security

+   * -I —Disables interaction
+    * -i —Prompts whether to remove each file
+    * -L —Sets wipe secure level to 0
+    * -p cnt —Performs wipe sequence cnt times, including random passes
+    * -r (or -R) —Repeats process for all files in any subdirectories
+    * -Ssize —Sets byte size for block device sector size (defaults to 512)
+    * -B —Disables percent reporting and some warnings
+    * -V —Shows percentage if file size is above a certain limit
+    * -v —Always shows percentage
+    * -Tsize —Block device buffer size (defaults to 4096)
+    * -tsize —Sets tiger hash input buffer size
+    * -xcnt —Enables random passes and (optionally) number of passes to perform
+    * -X —Disables random passes
+    * -Z —Overrides -x
+    * -z —Zeros out the file (fills it with zeros)
+    * -1num (vertical bar) —Sets generic security level to num