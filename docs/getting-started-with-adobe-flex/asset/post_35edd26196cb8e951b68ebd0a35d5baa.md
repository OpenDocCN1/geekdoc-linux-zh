
## Table 4.10 - Data-driven controls in Flex

| Control Name | Usage/ Description |
|---|---|
| List | A control which contains menus or cascading sub-menus. |
| HorizontalList | A horizontal bar holding menu items. |
| TileList | A subclass of PopUpButton control whose secondary button pops up a Menu control. |
| ComboBox | A drop down list of values from which a single value can be selected. |
| DataGrid | Equivalent to tables having multiple rows and columns. This is one of the mostly used data-driven controls. |
| Tree | This control helps to handle data in a hierarchical way. Each node can have its own sub-tree. |

In the next section, you will be shown some example of usage of both Menu-based and Data-Provider controls.

## 4.5 Exercises

We'll enhance the same application we've been working on in this chapter by putting more functionality in the middle tab. First we'll create a MenuBar control for different categories of products being offered by the company. Next we'll show details of category using a TileList control.

Follow these steps:

1. Rename "Tab 2" as "Products"
2. Define an XMLListCollection and create an XMLList to contain the data for the MenuBar. Initialize the menuBarCollection with menubarXML. The required code is shown below in Listing 4.6.

```actionscript
[Bindable]
public var menuBarCollection:XMLListCollection;
[Bindable]
private var menubarXML:XMLList = <>
<menuItem label="Vehicle">
<menuitem label="Sedan" data="Sedan"/>
<menuitem label="Truck" data="Truck"/>
<menuitem label="Van" data="Van"/>
</menuItem>
<menuItem label="Appliances">
<menuitem label="TV" data="TV"/>
<menuitem label="Freeze" data="Freeze"/>
</menuItem>
<menuItem label="Office Equipment">
<menuItem label="Printer" data="Printer"/>
<menuItem label="Scanner" data="Scanner"/>
<menuItem label="Copier" data="Copier"/>
</menuItem>
<menuItem label="Stationary">
<menuItem label="Pen" data="Pen"/>
<menuItem label="Cartige" data="Cartige"/>
<menuItem label="Scissor" data="Scissor"/>
</menuItem>
</>
private function initMenuBar():void {
menuBarCollection = new XMLListCollection(menubarXML);
}
```

### Listing 4.6 – Definition and initialization of data for the MenuBar

3. Put a MenuBar inside the Canvas. Assign the label of the Menu from the label of menubarXML, assign menuBarCollection as dataProvider. Also put a method itemClickHandler for the itemClick event. The corresponding code is shown below:

```xml
<mx:MenuBar labelField="@label" dataProvider="{menuBarCollection}"
itemClick="menuClickHandler(event)" />
</mx:MenuBar>
```

4. Put the definition of itemClick event handler as an empty method menuClickHandler for now:

```actionscript
private function menuClickHandler(event:MenuEvent):void {}
```

Now run the application. You will see a picture as shown below in Figure 4.12. Go ahead and try out the menu options.

![](img/c4119654311ebf24679359ca130a5ee6_90_0.png)

### Figure 4.12 – Example of Menu based control

5. Add a TileList and make it initially invisible with this code:

```xml
<mx:TileList id="myTileList" x="10" y="47" width="60%" visible="false" height="95%"> </mx:TileList>
```

6. Add the data along with some pictures for the TileList control. Also bind the tileListArray to ArrayCollection TileListDataProvider. The required code is shown in Listing 4.7.

```actionscript
[Bindable]
public var TileListDataProvider:ArrayCollection;
[Bindable]
 [Embed(source="vehicle 1.png")]
public var vehicle1:Class;
[Bindable]
 [Embed(source="vehicle 2.png")]
public var vehicle2:Class;
[Bindable]
 [Embed(source="vehicle 3.png")]
public var vehicle3:Class;
[Bindable]
 [Embed(source="vehicle 4.png")]
public var vehicle4:Class;
[Bindable]
 [Embed(source="vehicle 5.png")]
public var vehicle5:Class;
[Bindable]
 [Embed(source="vehicle 6.png")]
public var vehicle6:Class;
[Bindable]
 [Embed(source="vehicle 7.png")]
public var vehicle7:Class;
[Bindable]
 [Embed(source="vehicle 8.png")]
public var vehicle8:Class;
private var tileListArray:Array=[
(label: "Vehicle 1", data: 0, icon: "vehicle1"),
(label: "Vehicle 2", data: 1, icon: "vehicle2"),
(label: "Vehicle 3", data: 2, icon: "vehicle3"),
(label: "Vehicle 4", data: 3, icon: "vehicle4"),
(label: "Vehicle 5", data: 4, icon: "vehicle5"),
(label: "Vehicle 6", data: 5, icon: "vehicle5"),
(label: "Vehicle 7", data: 6, icon: "vehicle7"),
(label: "Vehicle 8", data: 7, icon: "vehicle8"),
];
[Bindable]
public var menuBarCollection:XMLListCollection;
```

### Listing 4.7 — Definition and initialization of data for TileList

7. Modify the menuClickHandler. Add some code to show the data from the above when the user clicks on the “Sedan” option. Also the same area should be cleared when another option is selected and the corresponding data should be rerendered. In this example TileList is hidden to make the example simpler. The code is shown in Listing 4.8.

```actionscript
private function menuClickHandler(event:MenuEvent):void {
    initSedanData();
    myTileList.visible = false;
    if ( event.item.@data == "Sedan" ){
        myTileList.visible = true;
        myTileList.dataProvider = TileListDataProvider;
    }
}
```

### Listing 4.8 – Rendering the data in TileList

Run the application again. Select “Sedan” from the menu option. You will see the pictures of your company’s products: beautiful cars. Isn’t that cool! *Figure 4.13* provides a sample output.

![](img/c4119654311ebf24679359ca130a5ee6_92_0.png)

### Figure 4.13 – Output from the TileList example

## 4.6 Summary

In this chapter you learned about the basics of components, the building blocks of a Flex application. First you learned about the class hierarchy of components; next you were introduced to Containers – placeholders for other Containers and Controls. The Application Container is the first component of any Flex application and it has some specific properties and attributes. The chapter then covered the other type of containers: Layout and Navigational.

The last section covered Controls. Controls are the means through which users interact with the application. There are different types of controls such as Text, Basic, Menu-Based and Data-Driven. The chapter showed some examples in detail from each category.

At this point, you should be more comfortable to build and work with Flex. In the next chapters we will work with more complex Flex applications.

## 4.7 Review questions

1. Name the ActionScript class name(s) which is superclass of most of the Flex components.
2. By default, size of an Application container is bigger than the contained components – why?
3. Can you place a control outside the visible area of the controller? How?
4. What is the HTML equivalent of the Grid Layout container?
5. What ActionScript method can be used to set the style of a component dynamically?
6. What is the default loading duration during Flex application after which the progress bar appears:
    - A. 100 millisecond
    - B. 1000 millisecond
    - C. 700 millisecond
    - D. 5 second
    - E. None of the above
7. Which of the following controls can be rendered using ActionScript only?
    - A. Label
    - B. Image
    - C. Menu
    - D. All of the above
    - E. None of the above
8. What is the name of the static method in Alert class used to display data?
    - A. display()
    - B. show()
    - C. init()
    - D. render()
    - E. None of the above
9. What are ways data can be provided to Flex control?
    - A. ArrayCollection object
    - B. XMLListCollection object
    - C. Both A & B
    - D. XMLText object
    - E. None of the above
10. You want to create a field where a user can choose his current state of residence as part of the address file – which of the following Data-driven controls should you use?
    - A. DataGrid
    - B. ComboBox
    - C. Tree
    - D. Any of the above
    - E. None of the above

## Chapter 5 - Binding data between controls

The Flex framework provides a robust structure built to maximize the facilitation of component-driven architectures. In the MVC (Model-View-Controller) architecture, the view and the controller are tied to the behavior of the model. In Component driven architecture, this approach is not feasible. In this case the user interface (UI) elements are built before the model, to provide reusability of the components across many different applications. In Flex we achieve this with what is called data binding.

In this chapter you will learn about:

- Data binding
- Different ways of data binding
- Data binding and storage mechanisms
- Data binding and UI controls

## 5.1 Data binding – The big picture

Data binding is a very interesting concept in Flex. It enables you to manage data more efficiently on the client side. Figure 5.1 provides an overview of data binding.

![](img/c4119654311ebf24679359ca130a5ee6_96_0.png)
