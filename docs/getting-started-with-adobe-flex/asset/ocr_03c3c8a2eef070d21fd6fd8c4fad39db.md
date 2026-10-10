```
]]>
</mx:Script>
```

**Listing 5.12 – Using ActionScript to create an ArrayCollection**

# 5.3.4.2 XMLListCollection

The XMLListCollection class provides collection functionality to the XMLList object and makes available some of the methods of the native XMLList class. The XMLList and the XMLListCollection class are mainly used to display trees and menu-based controls which have hierarchical data. The XMLListCollection class can be created both by using the MXML Tags and ActionScript class as shown in Listings 5.13 and 5.14 respectively.

```
<mx:XMLListCollection id="shapes">
    <mx:source>
        <mx:XMLList>
            <node label="Square" />
            <node label="Rectangle" />
            <node label="Circle" />
        </mx:XMLList>
    </mx:source>
</mx:XMLListCollection>
```

**Listing 5.13 - Using the `<mx:XMLListCollection>` tag to create an XMLListCollection**

```
<mx:Script>
    <![CDATA[
    import mx.collections.XMLListCollection;
    private var shapesXMLList:XMLList = new XMLList(<><node label='Square'/>
    <node label='Rectangle'/><node label='Circle'/></>);
    private var shapes:XMLListCollection;
    private function createXMLListCollection():void
    {
    shapes= new XMLListCollection();
    shapes.source = shapesXMLList;
    }
    ]]>
    </mx:Script>
```

**Listing 5.14 - Using ActionScript to create an XMLListCollection**

# 5.4 Data Driven UI Controls

Data-driven controls are key to any UI toolkit. Depending on whether the data is linear or hierarchical in nature, Flex provides different kinds of UI Controls:

+   - Scrolling List controls