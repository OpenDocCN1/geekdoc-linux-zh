# 15.4.2.7 Adding Management Tabs

The Website.py (shown in Appendix C) contains the manage_options variables, used to create additional tabs in the Zope management tab bar of instances of your product. Its code looks like this:

```
manage_options=OFS.Folder.Folder.manage_options(
    {'label': 'README', 'icon': 'icon', 'action': 'my_action', 'target': 'manage_main'},
)
```

To make sure you do not delete existing tabs from the Folder base class, open them using OFS.Folder.Folder.manage_options and then add your own tabs using +().

In this example, the line

```
#{'label':'README', 'icon': 'icon', 'action': 'README.txt', 'target': 'manage_main'},
```

is commented using the hash, or pound, symbol (#) because we do not need new tabs for our product (This line also appears in the product code with a hash symbol). To add your own tabs, you must define each in a dictionary, as described in the following table:

| Key Name | Value Description |
|---|---|
| label | Enter the text to appear on your tab. |
| icon | This assigns a special icon for your tab (optional). |
| action | Enter the page to be called when you click on the tab. |
| target | The value manage_main indicates that the action is to be displayed in the frame on the right of the Zope screen—this is standard when you click on a tab (optional). |

# 15.4.2.8 The Instance Methods in the Class

The instance methods in our class define the behavior and functionality of our class. The individual methods for the Website class can appear in any sequence. For example, Method A, called by Method B, need not appear first in the source text.

# 15.4.2.9 Securing the Instance Methods

When declaring an instance method for a class used in Zope, we must create the security assertion that controls access to the method. Instance methods in Zope have three modes of access control: public, private and protected. Public methods (including anonymous ones) are available to all users and can be called through the web by URL or from DTML or Python scripts. Private methods are restricted and may only be accessed from external Python code, such as products or external methods. Protected methods can only be called by users with a specific permission and, like public methods, they are web accessible.