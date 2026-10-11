•The “size” method returns the number of items in the list.

# ## Selecting Items

The first thing you need to decide is whether it is possible for the user to select only a single item at a time, or if multiple items can simultaneously be selected. This is controlled by the “selectmode” option: the default is only being able to select a single item (“browse”), while a selectmode of “extended” allows the user to select multiple items.

> *The names “browse” and “extended”, again for backwards compatibility reasons, are truly awful. This is made worse by the fact that there are two other modes, “single” and“multiple”which you **should not use** (they use an old interaction style that is inconsistent with modern user interface and platform conventions).*

To find out which item or items in the listbox the user has currently selected, use the “curselection” method, which will return the list of indices of all items currently selected; this may be an empty list, and for lists with aselectmode of “browse”, will never be longer than one item. You can also use the “selection includesindex” method to check if the item with the given index is currently selected.

To programmatically change the selection, you can use the “selection clear first ?last?” method to deselect either a single item, or any within the range of indices specified. To select an item, or all items in a range, use the “selection set first ? last?” method. Both of these will not touch the selection of any items outside the range specified.

If you do change the selection, you should also make sure that the newly selected item is visible to the user (i.e. it is not scrolled out of view). To do this, use the “see index” method.

When the selection is changed by the user, a “<ListboxSelect>” virtual event is generated. You can bind to this to take any action you need. Depending on your application, you may also want to bind to a double-click“Double-1” event, and use it to invoke an action with the currently selected item.

# ## Stylizing the List

Like most of the “classic” Tk widgets, you have immense flexibility in modifying the appearance of a listbox. As described in the reference manual, you can modify the font the listbox items are displayed in, the foreground (text) and background colors for items in their normal state, when selected, when the widget is disabled, and so on. There is also an “itemconfigure” method which allows you to change the foreground and background colors of individual items.

As is often the case, restraint is useful. Generally, the default values will be entirely suitable, and a good match for platform conventions. In the example we’ll get to momentarily, we’ll show how restrained use of these options can be put to good effect, in this case displaying alternate lines of the listbox in slightly different colors.

# ## Keeping Extra Item Data

The “listvariable” (or the internal list, if you’re managing things the old way) contains the strings that will be shown in the listbox. It’s very often the case though that each string in your program is associated with some other data item, and what you’re really interested in is not so much the string displayed in the listbox, but the associated data item. For example, a listbox containing names may be what is presented to the user, but your program is really interested in the user object (or id number) that is selected, not the particular name.

How can we associate this value with the displayed name? Unfortunately, the listbox widget itself doesn’t offer any facilities, so it’s something we’ll have to manage separately. There are a couple of obvious approaches. First, if the displayed strings are guaranteed unique, you could use a hash table to map the names to the associated object. So, given the name you can easily get the associated object. This probably wouldn’t work well for doing names, but could work for choosing countries for example.

A second approach is to keep a second list, parallel to the list of strings displayed in the listbox, which will hold the associated objects. So the first item in the strings list corresponds to the first item in the objects list, the second to the second, and so on. Any changes you make in one list (insert, delete, reorder) you need to make in the other. You can then easily map from the list item to the underlying object, based on their position in the list.