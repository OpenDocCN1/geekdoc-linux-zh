```
log.insert('end', msg)
log['state'] = 'disabled'
```

Note that because the widget was disabled, we had to reenable it to make any changes, even from our program.

# ## Formatting with Tags

Up until now, we've just dealt with plain text. Now it's time to look to how to add special formatting, such as bold, *italic*, **strikethrough**, background colors, font sizes, and much more. Tk's text widget implements these using a feature called tags.

Tags are objects associated with the text widget. Each tag is referred to via a name chosen by the programmer. Each tag can have a number of different configuration options; these are things like fonts, colors, etc. that will be used to format text. Though tags are objects having state, they don't need to be explicitly created; they'll be automatically created the first time the tag name is used.

# ### Adding Tags to Text

Tags can be associated with one or more ranges of text in the widget. As before, these are specified via indices; a single index to represent a single character, and a start and end index to represent the range from the start character to just before the end character. Tags can be added to ranges of text using the `tag add` method, e.g.

```
text.tag_add('highlightline', '5.0', '6.0')
```

Tags can also be provided when inserting text by adding an optional parameter to the “insert” method, which holds a list of one or more tags to add to the text you’re inserting, e.g.

```
text.insert('end', 'new material to insert', ('highlightline', 'recent', 'warning'))
```

As the text in the widget is modified, whether by the user or your program, the tags will adjust automatically. So for example if you had tagged the text “the quick brown fox” with the tag “nounphrase”, and then replaced the word “quick” with “speedy”, the tag would still apply to the entire phrase.

# ## Applying Formatting to Tags

Formatting is applied to tags via configuration options; these work similarly to configuration options for the entire widget. As an example:

```
text.tag_configure('highlightline', background='yellow', font=helvetica 14 bold', relief='raised')
```

The currently available configuration options for tags are: “background”, “bgstipple”, “borderwidth”, “elide”, “fgstipple”, “font”, “foreground”, “justify”, “lmargin1”, “lmargin2”, “offset”, “overstrike”, “relief”, “rmargin”, “spacing1”, “spacing2”, “spacing3”, “tabs”, “tabstyle”, “underline”, and “wrap”. Check the reference manual for detailed descriptions of these. The `tag cget` method allows you to query the configuration options of a tag.

Because multiple tags can apply to the same range of text, there is the possibility for conflict (e.g. two tags specifying different fonts). A priority order is used to resolve these; the most recently created tags have the highest priority, but priorities can be rearranged using the “tag raise” and “tag lower” methods.

# ## More Tag Manipulations

To delete a tag altogether, you can use the “tag delete” method. This also of course removes any references to the tag in the text. You can also remove a tag from a range of text using the “tag remove” method; even if that leaves no ranges of text with that tag, the tag object itself still exists.

72