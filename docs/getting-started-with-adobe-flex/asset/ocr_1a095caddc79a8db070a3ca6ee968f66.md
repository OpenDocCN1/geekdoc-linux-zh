# Chapter 5

+   1. In the MVC model, both the view and the controller and very tightly tied to the behaviour of the model. In the Component Driven architecture, the UI elements are built before the model in order to provide reusability.

+   2. `mx.controls.listClasses.ListBase`

+   3. The object must have a root node (parent) which wraps up all the descendant child nodes (leaf nodes).

+   4. The direction property of the `TileListControl` is used to determine whether it is a `horizontalTileList` or a `VerticalTileList`. The height and width of the individual tiles can also be set by setting the width of the `Tilelist` columns or the height of the `TileList` rows.

+   5. The `GroupingCollection` is used specifically in conjunction with `mx:dataprovider` tag to transform flat data into hierarchical data.

+   6. E – Zoomin is not an effect, though there is an effect by name zoom to apply zoom to the target component.

+   7. D – All of the Above

+   8. D, E – `XMLArray` and `XMLListCollection` are not valid ones.

+   9. D – `DataGrid` Control is not a scrolling List Control.

+   10. A, C and D. `DataGrid` is not one of the hierarchical controls.

# Chapter 6

+   1. As explained in the chapter, a trigger causes an effect to occur and an event makes a call to an Actionscript function or object. For example, a component can have a `focusOut` event and a `FocusOutEffect` trigger.

+   2. One of the most common filters applied to components in Flex is the `BevelFilter`. It is used to give a three-dimensional chiseled look to a component. For example:

```
```
<?xml version="1.0" encoding="utf-8"?>
<mx:Application xmlns:mx="http://www.adobe.com/2006/mxml"
		backgroundColor="0xFFFFF" layout="absolute">
	<mx:BevelFilter id="bevel" angle="45" highlightColor="0x00000f"
			shadowColor="0x000ff00" shadowAlpha="0.8" strength="15"
			quality="3" distance="7" highlightAlpha="0.7"/>
	<mx:Image source="@Embed(source='../location of imagsie/image.jpg')"
			filters="[bevel]"/>
</mx:Application>
```
```