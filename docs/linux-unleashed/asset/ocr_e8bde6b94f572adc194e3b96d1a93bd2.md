| Function | Description |
| :--- | :--- |
| accept | Once you have completed editing, you must use this option to save the changes to the file; otherwise the changes will not be written to the file. |
| doIt | Evaluates the highlighted text. |
| printIt | Prints a representation of the result of the evaluation at the current cursor position. |
| inspectIt | Invokes the Inspector view on the result. |
| search... | Enables you to search for a specific string. |
| goto... | Enables you to move to a specific location in the file. |
| font... | Enables you to change the font of the file. |
| indent... | Enables you to change the indenting of the file. |
| save as... | Enables you to save the file under a different name. |
| print | Prints the file. |


To select or highlight text, press the left mouse button over the first character and move the mouse (while holding the mouse button) to the end of the text you wish to select, and then release the mouse button. If you press the left mouse button again, the highlighting is removed and you can select something else.

To scroll through the text, use the scroll bars on the left of the view. By clicking the mouse below or above the thumb, the text scrolls one page for every click. If you press the Shift key at the same time as you click, the text scrolls to the position of the pointer in the scroll bar. This is useful for scrolling rapidly through long documents.

# Using the Inspector

The Inspector enables you to inspect an object. It consists of two subviews, one showing the names of the object's instance variables and the other showing the value of the selected instance variable. You can start an inspector by using the inspectIt function on the edit menu or by sending one of the following messages to an object:

```
anObject inspect
```

or

```
anObject basicInspect
```