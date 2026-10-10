

数据绑定是将一个对象（源）中的数据与另一个对象（目标）关联起来的过程。如图所示，当源对象发生变化时，通过触发事件，这些变化会自动反映到目标对象中。数据绑定提供了一种在应用程序不同层之间传递数据的便捷方式。它是生成代码、事件监听器和处理程序、错误捕获以及通过对象内省使用元数据的组合。在幕后，Flex 会代你生成大量代码。

## 5.2 实现数据绑定的方式

在 Flex 中有多种实现数据绑定的方式：

- 使用大括号（{}）语法
- 在大括号中使用 ActionScript 表达式
- 在 MXML 中使用 `<mx:binding>` 标签
- 在 ActionScript 中使用 **BindingUtils**

### 5.2.1 大括号（{}）语法

在下面的列表 5.1 中，一个文本控件从文本输入控件的属性获取数据。由于属性名位于大括号（{}）内，这意味着它是绑定表达式的源属性。每当源属性（myTextInput.text）发生变化时，Flex 都会将源属性的当前值复制到目标属性，即文本控件的 text 属性（myTextDestination）。

```xml
<mx:TextInput id="myTextInput" editable="true" enabled="true"/>
<mx:Text id="myTextDestination" text="{myTextInput.text}"/>
```

列表 5.1 – 使用大括号（{}）语法进行数据绑定。

### 5.2.2 大括号（{}）中的 ActionScript 表达式

大括号还可以包含 ActionScript 表达式。例如，它们可以包含对可绑定属性的计算和字符串连接。下列列表 5.2 说明了这种情况。

```xml
<mx:Model id="myBinding">
    <myBinding>
        <!-- Perform string concatenation. -->
        <a>This is {nameInput.text}</a>
        <!-- Perform a calculation. -->
        <b>{(Number(numberInput.text) as Number) + 100}</b>
    </myBinding>
</mx:Model>
<mx:Panel width="100%" height="100%" title="Binding expressions">
    <mx:Form>
        <mx:FormItem label="Name:">
            <mx:TextInput id="nameInput"/>
        </mx:FormItem>
        <mx:FormItem label="Enter a number:">
            <mx:TextInput id="numberInput" text="0"/>
        </mx:FormItem>
    </mx:Form>
    <mx:Text text="{'Concatenation: ' + myBinding.a}"/>
    <mx:Text text="{'Calculation: 100 + ' + numberInput.text+' = ' + myBinding.b}"/>
</mx:Panel>
```

列表 5.2 – 在大括号（{}）中使用 ActionScript 进行数据绑定。

### 5.2.3 MXML 中的 <mx:binding> 标签

`<mx:Binding>` 标签可作为大括号语法的替代方案使用。可以使用 `<mx:binding>` 标签的 source 属性提供源属性，并使用 destination 属性指定目标属性。`<mx:binding>` 标签还允许将一个源属性绑定到多个目标属性，或将多个源属性绑定到一个目标属性。我们也可以在 `<mx:binding>` 标签的 source 属性内部使用大括号（{}）。下列列表 5.3 提供了在 MXML 中使用 `<mx:binding>` 标签的示例。

```xml
<mx:Panel title="Data Binding Using mx Binding Tag">
    <mx:TextInput id="myTextInput" editable="true" enabled="true"/>
    <mx:Text id="myText" />
</mx:Panel>
<mx:Binding
    source="myTextInput.text"
    destination="myText.text"
/>
```

列表 5.3 – 使用 `<mx:binding>` 标签进行数据绑定。

### 5.2.4 ActionScript 中的绑定

也可以使用 mx.binding.utils.BindingUtils 类在 ActionScript 中实现数据绑定。我们可以使用 bindProperty() 方法或 bindSetter() 方法来完成数据绑定。这在下方的列表 5.4 中有所说明。

```xml
<?xml version="1.0" encoding="utf-8"?>
<mx:Application xmlns:mx="http://www.adobe.com/2009/mxml" width="200"
    height="200" initialize="initializeHandler();" >
    <mx:Script>
        <![CDATA[
        import mx.binding.utils.BindingUtils;
        private function initializeHandler():void
        {
            BindingUtils.bindProperty(myText, "text", myTextInput, "text");
        }
        ]]>
    </mx:Script>
    <mx:Panel
        title="Data Binding Using Action Script"
    >
        <mx:TextInput id="myTextInput" editable="true" enabled="true"/>
        <mx:Text id="myText" />
    </mx:Panel>
</mx:Application>
```

列表 5.4 – 在 ActionScript 中使用 BindingUtils 实现数据绑定

## 5.3 数据存储结构和机制

数据结构是原生的 Flash 数据类型，如 **Array**、**XML**、**XMLList**，或者 Flex 的任何数据集合，如 **ArrayCollection** 或 **XMLListCollection**。这些通常用于 ListBase 类的 **dataProvider** 属性中。ListBase 类（mx.controls.ListClasses.ListBase）是数据驱动控件的父类，它允许你在 Flex 应用程序中与数据进行交互。

### 5.3.1 Array

**Array** 是一种可以通过索引访问元素的数据结构。Array 类提供了一种有用的数据存储和检索机制。数组可以通过使用 MXML 标签或使用 ActionScript 来创建，如 *Listings 5.5* 和 *5.6* 分别所示。

```xml
<mx:Array id="shapes">
    <mx:String>Square</mx:String>
    <mx:String>Rectangle</mx:String>
    <mx:String>Circle</mx:String>
</mx:Array>
```

列表 5.5 – 使用 `<mx:Array>` 标签创建 Array。

```actionscript
<mx:Script>
    <![CDATA[
        public var colors:Array = ["Square", "Rectangle", "Circle"];
    ]]>
</mx:Script>
```

列表 5.6 – 使用 ActionScript 创建 Array。

### 5.3.2 XML

可以在 Flash 中创建 XML 对象来存储 XML 数据。XML 对象可以通过使用 MXML 标签或使用 ActionScript 来创建，如 List 5.7 和 5.8 分别所示。

```xml
<mx:XML id="shapes" >
    <node label="Shapes">
        <node label="Square" />
        <node label="Rectangle" />
        <node label="Circle" />
    </node>
</mx:XML>
```

列表 5.7 – 使用 `<mx:XML>` 标签创建 XML 对象

```actionscript
<mx:Script>
    <![CDATA[
        public var shapes:XML = <node
            label='Shapes'><node label='Square' /><node
                label='Rectangle' /><node label='Circle' /></node>;
    ]]>
</mx:Script>
```

列表 5.8 – 使用 ActionScript 创建 XML 对象

在上面的列表中，Shapes 节点充当 Square、Rectangle 和 Circle 子节点的父节点。没有后代的子节点称为叶节点。XML 对象必须有一个根节点（Parent）来包裹所有定义的子节点，才能成为有效的 XML。

### 5.3.3 XMLList

XMLList 与 XML 对象类似，不同之处在于 XMLList 对象不需要根节点来包裹后代节点。XMLList 对象可以通过使用 MXML 标签或使用 ActionScript 来创建，如 Listings 5.9 和 5.10 分别所示。

```xml
<mx:XMLList id="shapes" >
    <node label="Square" />
    <node label="Rectangle" />
    <node label="Circle" />
</mx:XMLList>
```

列表 5.9 – 使用 `<mx:XMLList>` 标签创建 XMLList 对象。

```actionscript
<mx:Script>
    <![CDATA[
        public var shapes:XMLList = <><node label='Square'/><node
            label='Rectangle' /><node label='Circle' /></>;
    ]]>
</mx:Script>
```

列表 5.10 – 使用 ActionScript 创建 XMLList 对象。

### 5.3.4 Flex 数据管理类

Flex 提供了一组称为 **collections**（集合）的数据管理类。集合可以非常高效地处理对数据集中的修改、添加和删除。集合使用上述讨论的数据类型（Array、XML、XMLList 等），并管理用户界面更新以反映底层数据的变化。在下面的部分中，我们将通过示例讨论其中几个集合类。

#### 5.3.4.1 ArrayCollection

ArrayCollection 类是一个包装类，它将 Array 作为集合暴露出来，并可以使用 ICollectionView 或 IList 接口的方法和操作来访问和操作。要使用 DataBinding，需要使用 ArrayCollection 类而不是 Array 类。ArrayCollection 提供了 Array 的所有功能以及更多功能。每个 ArrayCollection 类都包含一个作为数据源的 Array。ArrayCollection 类和底层的 Array 类主要用于显示扁平数据或线性数据。ArrayCollection 类可以通过使用 MXML 标签或 ActionScript 类来创建，如 *Listings 5.11* 和 *5.12* 分别所示。

```xml
<mx:ArrayCollection id="shapes">
    <mx:source>
        <mx:Array id="ShapeArray">
            <mx:String>Rectangle</mx:String>
            <mx:String>Square</mx:String>
            <mx:String>Circle</mx:String>
        </mx:Array>
    </mx:source>
</mx:ArrayCollection>
```

列表 5.11 – 使用 `<mx:ArrayCollection>` 标签创建 ArrayCollection

```actionscript
<mx:Script>
    <![CDATA[
        import mx.collections.ArrayCollection;
        private var shapesArray:Array = ["Square", "Rectangle", "Circle"];
        public var shapes:ArrayCollection;

        private function createArrayCollection():void
        {
            shapes= new ArrayCollection();
            shapes.source = shapesArray;
        }
    ]]>
</mx:Script>
```

