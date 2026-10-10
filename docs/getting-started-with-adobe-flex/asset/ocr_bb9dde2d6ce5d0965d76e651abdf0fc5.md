For data binding, as in the following example, curly braces are used. Curly braces cause the expression placed within it to be evaluated and the result gets assigned to the attribute of the MXML tag.

```
```xml
<mx:TextInput id="myText1" />
<mx:Text id="myText2" text="({myText1.text})" />
```
```

# 3.3.2 MXML Scripts

The other way in which ActionScript can be used in MXML is by using the <mx:Script> element:

```
```xml
<mx:Script>
</mx:Script>
```
```

The contents of <mx:Script> block must be enclosed within the CDATA construct, shown in the Listing 3.2, as this prevents the compiler from interpreting the content as XML and thus helping in proper generation of ActionScript code.

```
```xml
<mx:Script>
    <![CDATA[
        import mx.controls.Alert;
        private function result(evt:ResultEvent):void {
            Alert.show("Hello World!!!!");
        }
    ]]>
</mx:Script>
```
```

# Listing 3.2 - ActionScript using <mx:Script/> tag

The ActionScript code blocks can also be placed in a separate file with a .as extension. In this case the <mx:Script> element is used as shown below.

```
```xml
<mx:Script source="example.as" />
```
```

# 3.3.3 ActionScript Variables and data types

Variables are declared in ActionScript using the var keyword. The following syntax is used: var <var name> : <data type> ;

The data types supported in ActionScript are listed in Table 3.1 below. Every data type has certain properties and methods. You can also assign a value as you declare the variable. This is shown in the examples provided with Table 3.1.