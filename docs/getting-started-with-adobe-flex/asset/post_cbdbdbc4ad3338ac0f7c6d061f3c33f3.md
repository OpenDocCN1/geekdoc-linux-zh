
## 6.5 Filters

Filters allow you to apply an effect on a particular target component or a subset of target components. Without filters, all the effects defined in a transition are by default applied to all the target components.

For either a sequence or parallel effect, you can define the filter property. For example, if the filter property is specified a value of move, then the effect will apply only to those components whose x or y values change during the change of view state.

### 6.5.1 Common Filters

Some of the most commonly used values for the filter property as available in Adobe documentation are listed in Table 6.3 below.

| Value | Description |
| :---- | :---- |
| add | Specifies to play the effect on all children added during the change of view state. |
| hide | Specifies to play the effect on all children whose visible property changes from true to false during the change of view state. |
| move | Specifies to play the effect on all children whose x or y properties change during the change of view state. |
| remove | Specifies to play the effect on all children removed during the change of view state. |
| resize | Specifies to play the effect on all children whose width or height properties change during the change of view state. |
| show | Specifies to play the effect on all children whose visible property changes from false to true during the change of view state. |

Table 6.3 - Filter property value

### 6.5.2 Applying Filters

The filter property of the <mx:Sequence> or <mx:Parallel> tags can be set to any of the values defined in the above Table 6.3. The effect will then be played only on the target component or subset of components that satisfies that filter property. The concept of filters will become clear if you try adding a filter to the Parallel effect created in the previous sample application as shown in Listing 6.8.

```xml
<mx:Transition id="transition1" fromState="" toState="firstState">
    <mx:Parallel id="seq1" targets="{[panel1,txt1]}" filter="add">
        <mx:RemoveChildAction/>
        <mx:WipeDown duration="2000"/>
        <mx:AddChildAction/>
    </mx:Parallel>
</mx:Transition>
```

Listing 6.8 - Applying filters

When you run the sample application with the above change in the code, you can see that the wip edown effect only takes place for the TextArea which is the component that is added to the view state.

## 6.6 Exercises

You can experiment with states and transitions in this exercise. Let us create a simple display that shows various images of fruits. When you click on an image, you will get the details of that fruit.

1. Create a new Flex Project and an images folder in the project. In this example, images of fruits are added to this folder.
2. Go to the design view and add a Panel as shown below in Figure 6.8. This becomes the base state for the application.

![](img/c4119654311ebf24679359ca130a5ee6_127_0.png)

3. Next create a new state and name it ImagesState. This new state is based on the base state. Set this state as the start state of the application. Add six image components to the panel as shown below for this state. Also change the panel title to 'Fruits'. This is shown in Figure 6.9.

![](img/c4119654311ebf24679359ca130a5ee6_128_0.png)

**Figure 6.9 - Panel after adding images**

4. Provide the source for each of the images in the source property of the image component. Also add a click event to each image. The code after adding this state is shown in Listing 6.9 below.

```xml
<mx:states>
    <mx:State name="ImagesState">
        <mx:AddChild relativeTo="{panel1}" position="lastChild">
            <mx:Image id="image1" x="39" y="31" height="89" width="73" source="@Embed('images/lemon.jpg')" click="onImageClick(image1)" />
        </mx:AddChild>
        <mx:AddChild relativeTo="{panel1}" position="lastChild">
            <mx:Image id="image2" x="39" y="138" height="89" width="73" source="@Embed('images/apple.jpg')" click="onImageClick(image2)" />
        </mx:AddChild>
        <mx:AddChild relativeTo="{image1}" position="before">
            <mx:Image id="image3" x="144" y="138" height="89" width="73" source="@Embed('images/mango.jpg')" click="onImageClick(image3)" />
        </mx:AddChild>
        <mx:AddChild relativeTo="{panel1}" position="lastChild">
            <mx:Image id="image5" x="39" y="249" height="89" width="73" source="@Embed('images/papaya.jpg')" click="onImageClick(image5)" />
        </mx:AddChild>
        <mx:AddChild relativeTo="{panel1}" position="lastChild">
            <mx:Image id="image6" x="144" y="249" height="89" width="73" click="onImageClick(image6)" source="@Embed('../../images/watermelon.jpg')"/>
        </mx:AddChild>
        <mx:SetProperty target="{panel1}" name="title" value="Fruits"/>
        <mx:AddChild relativeTo="{panel1}" position="lastChild">
            <mx:Image x="144" y="31" width="73" height="89" source="images/orange.jpg"/>
        </mx:AddChild>
    </mx:State>
</mx:states>
```

Listing 6.9 - Adding state to the application

5. To show the details of the fruits, you can create one more new state and name it as descriptionState. This state is also based on the base state. Add an image component to display the image, a TextArea to give some description about the image and a back button to go back to the previous state. Also change the panel title to 'Fruit Description'. This is illustrated in *Figure 6.10*. Note the figure shows at the top left corner a little image. This indicates that the source for the image has not been specified yet.

![](img/c4119654311ebf24679359ca130a5ee6_129_0.png)

**Figure 6.10 - Adding the second state - descriptionState**

6. The source code after adding this state is as shown in *Listing 6.10* below.

```xml
<mx:State name="descriptionState">
    <mx:AddChild relativeTo="{panel1}" position="lastChild">
        <mx:Image id="mainImage" x="0" y="0" width="252" height="169"/>
    </mx:AddChild>
    <mx:AddChild relativeTo="{panel1}" position="lastChild">
        <mx:TextArea id="textArea" x="10" y="197" height="106" width="232"/>
    </mx:AddChild>
    <mx:AddChild relativeTo="{panel1}" position="lastChild">
        <mx:Button x="99" y="321" label="Back" click="buttonClick()"/>
    </mx:AddChild>
    <mx:SetProperty target="{panel1}" name="title" value="Fruit Description"/>
</mx:State>
```

Listing 6.10 - Source code after adding the new state

Some ActionScript code needs to be added to display the corresponding description for each image. Keep it simple by storing the description as XML data. Also the state change between the two states have to be managed in the ActionScript code as shown in *Listing 6.11* below.

```actionscript
<mx:Script>
    <![CDATA[
    import mx.controls.Alert;
    [Bindable]
    private var results:XMLList;
    private var text:XML = <image>
    <image id="image1"
        description="The lemon is a small evergreen tree (Citrus limon) originally native to Asia, and is also the name of the tree's oval yellow fruit. The fruit is used for culinary and nonculinary purposes throughout the world - primarily for its juice, though the pulp and rind (zest) are also used, mainly in cooking and baking. Lemon juice is about 5% (approximately 0.3 mole per litre) citric acid, which gives lemons a sour taste, and a pH of 2 to 3. This makes lemon juice an inexpensive, readily available acid for use in educational science experiments. Because of the sour flavor, many lemon-flavored drinks and candies are available, including lemonade and sour heads."/>
    <image id="image2" description="Give the description here"/>
    <image id="image3" description="Give the description here"/>
    </image>;

    private function onImageClick (image:Image):void {
        var item:XML;
        currentState='descriptionState';
    ]]>
</mx:Script>
```

Listing 6.11 - ActionScript code for state changes and descriptions
