Use customized color for grep colorization. <slot> specifies which part of the line to use the specified color, and is one of

+   context
+   non-matching text in context lines (when using -A, -B, or -C)

+   filename
+   filename prefix (when not using -h)

+   function
+   function name lines (when using -p)

+   linenumber
+   line number prefix (when using -n)

+   match
+   matching text (same as setting matchContext and matchSelected)

+   matchContext
+   matching text in context lines

+   matchSelected
+   matching text in selected lines

+   selected
+   non-matching text in selected lines

+   separator
+   separators between fields on a line (:, -, and =) and between hunks (—)

color.interactive

When set to always, always use colors for interactive prompts and displays (such as those used by “git-add —interactive” and “git-clean —interactive”). When false (or never), never. When set to true or auto, use colors only when the output is to the terminal. Defaults to false.

color.interactive.<slot>

Use customized color for git add —interactive and git clean —interactive output. <slot> may be prompt, header, help or error, for four distinct types of normal output from interactive commands.

color.pager

A boolean to enable/disable colored output when the pager is in use (default is true).

color.showBranch

A boolean to enable/disable color in the output of (1). May be set to always, false (or