# View method

# Description

| manage_UndaFarm | Shaws the standard Unda infarmation and allows users to actions carried out on the object (ar subobjects). |

| manage_access | The method used for the Security tab. Allows Zope managers to change permissions and rules. |

| manage_main | The main object management screen. The Cents tab for folderish objects; for non-folderish it is usually the Edit tab. |

| manage_owner | The method used for the Ownership tab. Allows changes to object ownership. |

| properpertyheets/Book_description/manage | The property management interface. Each property sheet your ZClass has its own manage method. |

Because you need a view that will allow you to edit the book instances, properpertyheets/Book_description/manage, the method for managing the property sheet for this ZClass (see Figure 9-20).

+   4. Click Add.

Zope now creates a management tab called Properties, which appears in the tab bar when you click an object in ZClass (visible in Figure 9-25 on page 176). Clicking this calls the method properpertyheets/Book_description/manage for the book instance, allowing you to change its properties.

By default, the BookClass has a Contents view that calls the Python method manage_main. This view and the manage_main method are inherited from the ObjectManager base class we select for BookClass. Zope uses the manage_main method to display the contents of the object in the management screen.

Table 9-1 (page 166) shows the views Zope automatically creates when you select certain classes.

![](bbox=[0.198, 0.64, 0.915, 0.88])

Figure 9-20: Management screen after creating the view