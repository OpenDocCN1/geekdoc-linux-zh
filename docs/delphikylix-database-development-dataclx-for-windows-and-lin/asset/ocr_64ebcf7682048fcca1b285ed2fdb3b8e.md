# TABLE 5.7  Continued

| Stored Value | EditMask | Displayed Value | Remarks |
| --- | --- | --- | --- |
| 33467-0708 | 00000-0000;1;_- | 33467-0708 | ZIP code. Hyphen is stored. |
| 5/28/01 | !99/99/00;1;_- | 5/28/01 | Date. Slashes are stored. Extra spaces are stored at the beginning of the string rather than at the end. |

NOTE

The built-in Delphi edit masks leave something to be desired if you're wanting to use anything more than a simple edit mask. The standard data-aware components don't validate complex masks well (such as phone numbers, Social Security numbers, and the like). For this reason, you might want to consider a third-party library to assist you with data entry and validation. I use Orpheus, from TurboPower Software Company. You can find TurboPower's Web site at http://www.turbopower.com.

# Simple Data-Aware Components

Most data-aware components fall into a category that I've defined as simple data-aware components. For purposes of this discussion, a simple data-aware component is one that links to a single field in a single record of a single dataset. For instance, a component that enables you to display and edit values for the FirstName field of a dataset is a simple data-aware component.

This contrasts with more complex data-aware components; which either display multiple values from the same dataset (such as TDBGrid), or which look up information from one dataset for inclusion in another dataset (such as TDBLookupComboBox and TDBLookupListBox).

In this section, I'll discuss the simple data-aware components, and following sections will cover some that are more complex. Don't be too concerned at this point with the mechanics of creating data-aware components. Near the end of this chapter, I'll show you how to take a non-data-aware component and create a data-aware descendent from it.

# TDBText

TDBText is the simplest of all the data-aware components. It is a display-only component, similar to the standard TLabel. To use it, drop a TDBText component on a form, and set the DataSource and DataField properties. The data is displayed according to the output format discussed in the preceding section.

![](bbox=[0.88, 0.82, 0.99, 0.95])