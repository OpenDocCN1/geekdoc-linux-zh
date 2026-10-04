# Chapter 10. The text Widget and html_library

However, the last `insert` command inserts text at location 2.0 and terminates that text with a newline, pushing the line that was at index 2.0 down to index 3.0.

# 10.3.2 Searching Text

A script can search for text within a text widget using the `textName search` subcommand. This command will search forward or backward from an index point or search between two index points.

**Syntax:** `textName search ?options? pattern startIndex ?end-Index`

+   - textName: The name of the text widget.

+   - search: Search the contents of this text widget for text that matches a particular pattern.

+   - ?options?: Options for search include:

**Search Direction** These are mutually exclusive options.

+   - -forwards: The direction to search from the `startIndex`.

+   -backwards

**Search Style** These are mutually exclusive options.

+   - -exact: Search for an exact match.

+   - -regexp: Use regular expression rules to match the `pattern` to text.

+   - -nocase: Ignore the case when comparing `pattern` to the text.

**Other Options** These are not mutually exclusive options.

+   - -count varName: The `-count` option must be followed by a variable name. If the search is successful,