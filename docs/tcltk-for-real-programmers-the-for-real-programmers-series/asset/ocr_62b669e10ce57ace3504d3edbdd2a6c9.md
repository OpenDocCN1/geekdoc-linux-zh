# Chapter 8. Introduction to Tk Graphics

end or last The bottom entry in the menu. If the menu has no entry, this is the same as none.

@number The entry that contains (or is closest to) the Y-coordinate defined by number.

pattern The first entry with a label that matches the glob style pattern.

Syntax: menuName insert index type ?options?

menuName insert Insert a new entry before position index.

index The position to insert this entry before.

Syntax: menuName delete index1 index2

menuName delete Delete menu entries.

index1 index2 Delete the entries between the numeric indices index1 and index2, inclusive.

Syntax: menuName index string

menuName index Return the numeric index of the menu entry with the label string.

string The string displayed in a -label option for a menu entry.

The following example shows how the various menus are created and how they look. In actual fact, you cannot pull down all the menus at once. however, use the tear-off strip (select the dotted line at the top of the menus) to create a new window and have multiple windows displayed.

# Example 8.8.2-1

```
Example Script
#--------------------------------------------------------------------------------
# Create a checkbox menu - Place it on the left
#
```