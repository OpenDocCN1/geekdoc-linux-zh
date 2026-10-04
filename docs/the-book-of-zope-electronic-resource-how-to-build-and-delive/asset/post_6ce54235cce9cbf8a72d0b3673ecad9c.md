
However, these error messages can be misleading, often a missing quote on an attribute or missing right bracket at the end of a dhtml tag can cause the rest of the dhtml code to be ignored. In this case, the tag with the actual error is not the one specified in the error message. For example, look at this incorrect dhtml code:

```html
<html-if name="today">
  Yesterday was <dhtml-var expr="(today-1).day()>
</dhtml-if>
```

In Line 2, the quote is missing at the end of the expr attribute. However, the error Zope returns when you try to save this

`No closing tag, for tag dhtml-if name="today", in line 1`

As you can see, line 3 does contain a closing tag for the dhtml-if in line 1. The problem is that Zone thinks this line is part of the value of the expression attribute from line 2 because there is no closing quote after day(), so Zone doesn't recognize line 3 as a dhtml tag at.

## 16.2.2 Debug Mode

When debug mode is activated in Zope (which is if you use the default Zope start script) you will see a traceback of the error after the text of the error page. Otherwise, the traceback is displayed in the HTML source of the page, and you can view it by choosing View Page Source or View Frame Source after right-clicking on the error page.

The traceback shows the route of execution from the module that caused the exception (always the bottom file in the traceback) to the module that controls Zope output, as well as the objects or expressions executing in each module at the time of the error. (A more detailed description of exceptions is given in section 16.3.1 below.)

In the case of DHTML errors, the final module is always

```python
/usr/local/Zope-x.x.x/src/lib/python/DocumentTemplate/DT_String.py,
```

as shown in Figure 16-1. Unfortunately, this also makes the traceback less useful for debugging DHTML. The error message and the objects shown in the traceback must be sufficient to locate the error.

You can greatly enhance the information provided by Zope error messages by installing the ZDebug product. Although still in development in this writing, it is still a highly useful tool for debugging. Download it from http://www.zope.org/Members/hathazard/ZDebug.

## 16.3 Errors Specific to Zope

The error messages listed in Table 16-2 are specific to Zope.

Table 16-2: Error Messages Specific to Zope

| Error | Explanation |
| --- | --- |
| Bad Request | An invalid request was entered. |
| CopyError | The object cannot be copied. |
| DateTimeError | There is an error in the date or time format. |
| Forbidden | This action is forbidden. |
| HistorySelectionError | An error occurred when working with a history function. |
| InError | An error occurred when working with the In-tag. |
| Invalid Object Name | The object was not found in the module. |
| Invalid Permission | The permission is invalid. |
| MailHostError | A mailhost-specific error occurred. |
| ModuleError | The module cannot be accessed. |
| ParseError | A syntax error in a DTML object occurred. |
| SuperCannotOwn | A superuser cannot own objects. |
| Time Error | An invalid time was specified. |
| Type Errors | This type already exists. |
| Unauthorized | Unauthorized use or access to an object was attempted. |
| UndoError | An error occurred during an undo action. |
| ValidationError | A parameter is invalid. |
| VersionError | An error occurred when using a version function. |

## 16.3.1 Zope Error Messages

Following are some examples of Zope error messages as they occur in practice:

AttributeError

An object attribute cannot be accessed.

```
Error Type : AttributeError
Error Value : 'string' object has no attribute x
```

Explanation: An attempt was made to call the attribute x in a string, but there is no attribute by that name. This error can also occur if the attribute exists, but it is private to the object and not published through Zope.

> The AttributeError and SystemError occur more frequently when you are working with Zope but actually belong to the standard Python errors.

## Bad Request

This type of error indicates that an HTTP request is not valid, For example:

Error Value: The id ___ contains characters illegal in URLs.

Explanation: The specified id contains illegal characters.

Error Value: The id index html is invalid - it is already in use.

Explanation: An attempt was made to assign an existing id name (in this case: index_html).

## CopyError

You cannot copy an object. This may be because copying is not permitted by the object you want to copy, or the object to which you want to copy the object cannot accept the new object.

The object ___ does not support this operation.

Explanation: The selected object does not support copying.

Cannot paste into this object.

Explanation: You cannot paste this object into this folderish object because it cannot not contain the type of object(s) you have in the clipboard.

## DateTimeError:

A specified time zone does not exist, or a time was specified in the wrong format.

Unrecognized timezone

Explanation: The time zone used is not recognized.

Unknown time zone in date

Explanation: The specified date contains a time format that does not exist or that is not supported.

Invalid date

Explanation: The specified date format is not valid.

## Forbidden

An action is forbidden. This may be because the user does not have appropriate permissions.

Zape Error
Error Type : Forbidden
Error Value : You are not authorized

## SelectionError

The selected action cannot be carried out (see section 3.1.5 history management).

No historical revision was selected.
Explanation: No element history list was selected.

Only one historical revision can be copied to the present.
Explanation: More than one element in the history list was selected.

Only two historical revisions can be compared.
Explanation: An attempt was made to compare more than two elements in the history list.

## InError

Problems occurred when processing In tag. See section 4.13.10, "The In tag."

Error Value: Strings are not allowed as input to in tag.
Explanation: An attempt was made to use In tag in a string, which is forbidden.

## Invalid Object Name

An object or a method cannot be found in the specified module. For example, assume you create an external method, and either write the name of the Python module incorrectly or are not currently in the Extensions directory.

The specified object, test_obj, was not found in module.

## KeyError

This can occur when you attempt to access an object from the namespace using the [...] notation and the name is not found. This error also occurs in any dictionary lookup attempted with a key that is not in the dictionary or mapping (dictionary-like) object (such as a Zope folder or the REQUEST object).

A key was not found in the namespace. Either it was entered incorrectly or it does not exist.

Check the spelling of the variables listed in the error message. Remember that Zope and Python names are case sensitive.

## MailHostError

An error occurred when sending electronic mail via a MailHost object. For more information, see section 4.3.12, "The Sendmail tag."

No mailhost was not specified in tag

Explanation: The mail host was not specified in the Sendmail tag.

An unsupported encoding was specified in tag

Explanation: An incorrect or unsupported value was set for the encode parameter.

## Module Error

You cannot access a module.

The specified module, TestModule, couldn't be found.
The specified module, TestModule, couldn't be opened.

Explanation: This error occurs when you try to create an external method and either write the name of the Python module incorrectly or are not currently in the Extensions directory.

## ParseError

Parse errors occur when you try to save an object (a DTML method or DTML document) that contains errors. You cannot save objects before any parse errors have been resolved, such as the following:

unexpected end tag

Explanation: An end tag exists that is not needed or is in the wrong location.

+   Explanation:more than one else tag for a single if tag
No more than one else block is allowed

+   Explanation:Two or more else tags were used in an if block.
The __ attribute was used but neither of the start, end, or size
