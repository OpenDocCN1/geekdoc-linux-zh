the top level of the tree named by \textless dataref\textgreater .
'ls' SP \textless dataref\textgreater SP \textless path\textgreater LF
See filemodify above for a detailed description of \textless path\textgreater .
Output uses the same format as git ls-tree \textless tree\textgreater --- \textless path\textgreater :
\textless mode\textgreater SP ('blob' | 'tree' | 'commit') SP \textless dataref\textgreater HT \textless path\textgreater LF
The \textless dataref\textgreater represents the blob, tree, or commit object at \textless path\textgreater and can be used in later cat-blob, filemodify, or ls commands.
If there is no file or subtree at that path, git fast-import will instead report missing SP \textless path\textgreater LF
See“Responses To Commands” below for details about how to read this output safely.

# **feature**

Require that fast-import supports the specified feature, or abort if it does not.
'feature' SP \textless feature\textgreater e ('=' \textless argument\textgreater)? LF
The \textless feature\textgreater part of the command may be any one of the following:
date-format, export-marks, relative-marks, no-relative-marks, force
Act as though the corresponding command-line option with a leading \textemdash{} was passed on the command line (see OPTIONS, above).
import-marks, import-marks-if-exists
Like \textemdash{}import-marks except in two respects: first, only one “feature import-marks” or “feature import-marks-if-exists” command is allowed per stream; second, an \textemdash{}import-marks= or \textemdash{}import-marks-if-exists command-line option overrides any of these “feature” commands in the stream; third, “feature import-marks-if-exists” like a corresponding command-line option silently skips a nonexistent file.
cat-blob, ls
Require that the backend support the cat-blob or ls command. Versions of fast-import not supporting the specified command will exit with a message indicating so. This lets the import error out early with a clear message, rather than wasting time on the early part of an import before the unsupported command is detected.
notes
Require that the backend support the notemodify (N) subcommand to the commit command. Versions of fast-import not supporting notes will exit with a message indicating so.
done
Error out if the stream ends without a done command. Without this feature, errors causing the frontend to end abruptly at a convenient point in the stream can go