# 2.5.1.4 Modifying Standard Objects

You can modify these standard objects to suit your own needs, but if you do, you must observe the acquisition mechanism. Remember that changing the contents of any methods in the root directory affects all objects that use that method.

To change only the appearance of specific objects, copy the applicable methods (see section 2.4.3), for example standard_html_header, to the folder at or above the objects you want to change, change the copied methods. Thus, only the objects in the folder containing the changed methods (or in folders below) will be affected by the modifications; all other objects will still use the original methods.

# Summary

You are now familiar with creating and manipulating objects in Zope. The next chapter will take you through Zope's tab bar and different management screens.