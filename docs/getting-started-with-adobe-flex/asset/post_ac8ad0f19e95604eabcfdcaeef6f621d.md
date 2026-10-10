
- A. The Curly Braces ({}) Syntax
- B. ActionScript expressions
- C. <mx:binding> tag in MXML.
- D. BindingUtils in ActionScript
- E. All of the above

7. Which of the following are the different types of Item Renderers?
- A. Drop-In item renderers
- B. Inline item renderers
- C. Custom item renderers
- D. All of the above
- E. None of the above

8. Which of the following is NOT a basic data storage mechanism in Flex?
- A. Array
- B. XML
- C. XMLList
- D. XMLArray
- E. XMLListCollection

9. Which of the following is Not a scrolling Control in Flex?
- A. List Control
- B. HorizontalList Control
- C. TileList Control
- D. DataGrid Control
- E. None of the above

10. Which of the following are the hierarchical controls that Flex provides?
- A. Menu Control
- B. Tree Control
- C. DataGrid Control
- D. MenuBar Control
- E. All of the above

## Chapter 6 - Working with view states, transitions and filters

In this chapter, you will learn the basics of how to change the look and feel of the application interface based on the task that a user is performing. Example of this includes changing the image of an icon when a user rolls a mouse over it. Using view states, transitions and filters, rich internet applications can be built without much hassle.

In this chapter you will learn about:

- View states
- Using components with states
- Using effects
- Using transition
- Using filters in effects

### 6.1 Working with view states, transitions and filters: The big picture

View states allow you to change the appearance of an application in response to some user action. Transitions allow you to define, how this change in the view state appears to the user on screen. A transition is defined with the help of effect classes, in combination of different effects that are designed specifically to handle transitions. Figure 6.1 provides an overview of the relationship between these concepts.

![](img/c4119654311ebf24679359ca130a5ee6_114_0.png)

![](img/c4119654311ebf24679359ca130a5ee6_115_0.png)

In the figure, *View State 1* is the initial state of the UI. When the defined *transition* is applied to this view state the UI changes to *View State 2*. A transition is defined using different effects (*Effect 1, Effect 2... Effect N*). These effects can be applied conditionally using different *filters* along with effects. Filters are used to conditionally apply the defined effects only on a subset of target components defined in the *transition*.

### 6.2 View states

*States* are a collection of changes to a view. Let us say that we have a view with many components (containers and controls). Then, if any change occurs to the layout of any of these view components, then it becomes a view state. Every component that inherits the `UIComponent` class will have view states and these components will inherit the states property.

#### 6.2.1 Creating States

States can be easily created in Flex Builder using the design view. Let us see how this can be done using a simple example. Follow these steps:

1. Create a new Flex project.

2. Switch to design view and using the layout tools, add two components, a panel and a button as shown in *Figure 6.2* below. This now becomes the base state of the application.

![](img/c4119654311ebf24679359ca130a5ee6_115_1.png)

3. Now you can create a new state based on this base state. Select *Window -> Show View -> States* to open the States view. *Figure 6.3* shows the States view. Now click on the *New State* icon as shown in the below figure. A popup window appears. Name the new state as *firstState* and then specify the component on which it is based. In this example it is based on the `<base state>`. You can optionally tick the ‘set as Start state’ option if this state should be the start state. Leave that option un-ticked for the time being since we want the base state as the start state.

![](img/c4119654311ebf24679359ca130a5ee6_116_0.png)

**Figure 6.3 - States View**

4. Now add a TextArea to this new state and define some properties for the TextArea as shown below.

```xml
<mx:TextArea id="txt1" x="10" y="10" width="260" height="210"
 text="My First State" fontSize="20" textAlign="center"
 backgroundColor="#FFEA00"/>
```

5. You can add one more state in the same manner as shown earlier in Figure 6.3 and name it *secondState*. Add as many states as you would like. You can even add multiple components of your choice to each new state.

6. You can check the source view to see what happened behind the scenes while we created these new states and added components to them. Listing 6.1 shows you the code that is generated.

```xml
<mx:Panel id="panel1" x="0" y="0" width="300" height="300"
 layout="absolute" title="Learn how to change states">
 <mx:Button x="99" y="228" label="Change"
 click="onClick(event)"/>
</mx:Panel>
<mx:states>
 <mx:State name="firstState">
 <mx:AddChild relativeTo="[panel1]" position="lastChild">
 <mx:TextArea id="txt1" x="10" y="10" width="260"
 height="210"
 text="My First State" fontSize="20" textAlign="center"
 backgroundColor="#FFEA00"/>
 </mx:AddChild>
 </mx:State>
 <mx:State name="secondState">
 <mx:AddChild relativeTo="[panel1]" position="lastChild">
 <mx:TextArea id="txt2" x="10" y="10" width="260"
 height="210"
 text="My Second State" fontSize="20" textAlign="center"
 backgroundColor="#0036FF"/>
 </mx:AddChild>
 </mx:State>
</mx:states>
```

**Listing 6.1 - Defining states**

7. Now add an event handler to the button in the source view to toggle between the current states. The ActionScript code is shown in Listing 6.2 below.

```actionscript
<mx:Script>
    <![CDATA[
    private function onClick(e:MouseEvent):void{
        if (currentState=='firstState')
            currentState='secondState';
        else if(currentState=='secondState')
            currentState='firstState';
        else
            currentState='firstState';
    }
    ]]>
</mx:Script>
```

**Listing 6.2 - Code to toggle between states**

8. Run the application and you can see the output as shown in Figure 6.4. This is the base state of the application.

![](img/c4119654311ebf24679359ca130a5ee6_117_0.png)

9. Now click on the *change* button and you can see the first state that you created as shown in *Figure 6.5*.

![](img/c4119654311ebf24679359ca130a5ee6_118_0.png)

**Figure 6.5 - State when the user clicks the *change* button for the first time**

10. Click again on the *Change* button and you can view the second state as shown in *Figure 6.6*.

![](img/c4119654311ebf24679359ca130a5ee6_118_1.png)

**Figure 6.6 - State when the user clicks the *Change* button for the second time**

11. Creating different states is simple by using the design view but you need to know all the code that is created in the background. So let us have a look at these new tags.

##### 6.2.1.1 The <mx:states> tag

The states property defines an array of view states for a view component. Every view component will have a base state, which is the first state. The base state is the default state of any Flex application. The states property cannot be specified on any child controls. It can only be specified on the root of a custom control or application.

##### 6.2.1.2 The <mx:State> tag

A State object can be added to the state property of the component. Adding so, will create new view states for that component.

Syntax of the <mx:State> tag:

```xml
<mx:State basedOn="null" name="null" overrides="null"/>
```

The basedOn attribute specifies the view state on which it is based on and the name attribute specifies the name of the current State object. The purpose of a state is to alter the appearance of a component in response to a user or system-initiated event, for example, the click of a button. Altering the appearance of a component involves the use of overrides via a state. Valid overrides include:

- AddChild
- RemoveChild
- SetEventHandler
- SetProperty
- SetStyle

#### 6.2.2 State properties, style and events

In order to further customize a state in terms of look and feel and behavior, the following tags can be used.

##### 6.2.2.1 The <mx:SetEventHandler> tag

The <mx:SetEventHandler> tag allows you to create event listeners that are active only during a specific state. This is made possible by using the handler event type or the handlerFunction property.

In the handler event type, you can specify more than one parameter for the event listener function. You can even add ActionScript code within the tag instead of providing an event listener function. This is shown in the example below:

```xml
<mx:SetEventHandler target="(Button)" name="ButtonClick"
    handler = "buttonHandler(event, linkButtonID)"/>
```
