# # EDITING PATCHES

Invoking git add -e or selecting e from the interactive hunk selector will open a patch in your editor; after the editor exits, the result is applied to the index. You are free to make arbitrary changes to the patch, but note that some changes may have confusing results, or even result in a patch that cannot be applied. If you want to abort the operation entirely (i.e., stage nothing new in the index), simply delete all lines of the patch. The list below describes some common things you may see in a patch, and which editing operations make sense on them.

+   - added content
+   
+     Added content is represented by lines beginning with “+”. You can prevent staging any addition lines by deleting them.

+   - removed content
+   
+     Removed content is represented by lines beginning with “-“. You can prevent staging their removal by converting the “-” to a “ ” (space).

+   - modified content
+   
+     Modified content is represented by “-” lines (removing the old content) followed by “+” lines (adding the replacement content). You can prevent staging the modification by converting “-” lines to “, and removing “+” lines. Beware that modifying only half of the pair is likely to introduce confusing changes to the index.

There are also more complex operations that can be performed. But beware that because the patch is applied only to the index and not the working tree, the working tree will appear to “undo” the change in the index. For example, introducing a new line into the index that is in neither the HEAD nor the working tree will stage the new line for commit, but the line will appear to be reverted in the working tree.

Avoid using these constructs, or do so with extreme caution.

+   - removing untouched content
+   
+     Content which does not differ between the index and working tree may be shown on context lines, beginning with a “ ” (space). You can stage context lines for removal by converting the space to a “-“. The resulting working tree file will appear to re-add the content.

+   - modifying existing content
+   
+     One can also modify context lines by staging them for removal (by converting “ ” to “-“) and adding a “+” line with the new content. Similarly, one can modify “+” lines for existing additions or modifications. In all cases, the new modification will appear