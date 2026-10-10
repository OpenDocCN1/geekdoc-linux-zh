# 5.3.2 XML

XML objects can be created in Flash to store XML data. XML objects can be created either by using MXML tags or by using ActionScript as shown in Listings 5.7 and 5.8 respectively.

```
<mx:XML id="shapes" >
    <node label="Shapes">
        <node label="Square" />
        <node label="Rectangle" />
        <node label="Circle" />
    </node>
</mx:XML>
```

**Listing 5.7 – Using the <mx:XML> tag to create an XML object**

```
<mx:Script>
    <![CDATA[ 
        public var shapes:XML = <node 
            label='Shapes'><node label='Square' /><node 
                label='Rectangle' /><node label='Circle' /></node>; 
    ]]>
</mx:Script>
```

**Listing 5.8 – Using ActionScript to create an XML Object**

In the above listing, the Shapes node acts as the parent node to the Square, Rectangle and Circle child nodes. Child nodes with no descendants are called leaf nodes. An XML object must have a root node (Parent) which wraps up all the defined child nodes for it to be a valid XML.

# 5.3.3 XMLList

An XMLList is similar to an XML object except for the fact that an XMLList object doesn't need a root node to wrap up the descendant nodes. XMLList objects can be created either by using MXML tags or by using ActionScript as seen in Listings 5.9 and 5.10 respectively.

```
<mx:XMLList id="shapes" >
    <node label="Square" />
    <node label="Rectangle" />
    <node label="Circle" />
</mx:XMLList>
```

**Listing 5.9 – Using the <mx:XMLList> tag to create an XMLList object.**

```
<mx:Script>
    <![CDATA[ 
        public var shapes:XMLList = <>><node label='Square'/><node 
            label='Rectangle' /><node label='Circle' /></>; 
    ]]>
```