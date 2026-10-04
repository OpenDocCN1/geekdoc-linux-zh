# 16.3 Errors Specific to Zope

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

# 16.3.1 Zope Error Messages

Following are some examples of Zope error messages as they occur in practice:

AttributeError

An object attribute cannot be accessed.

```
Error Type : AttributeError
Error Value : 'string' object has no attribute x
```

Explanation: An attempt was made to call the attribute x in a string, but there is no attribute by that name. This error can also occur if the attribute exists, but it is private to the object and not published through Zope.

> The AttributeError and SystemError occur more frequently when you are working with Zope but actually belong to the standard Python errors.