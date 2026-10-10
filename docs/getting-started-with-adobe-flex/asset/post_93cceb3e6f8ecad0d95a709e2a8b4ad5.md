
However, if the *handlerFunction* property is used, the event listener function will only take one event object as parameter as shown below.

```xml
<mx:SetEventHandler target="(Button)" name="ButtonClick"
     handlerFunction="buttonHandler"/>
```

### 6.2.2.2 The <mx:setProperty> tag

The <mx:setProperty> tag is used to set the value of some property that will hold for a particular view state:

```xml
<mx:SetProperty target="(container)" name="alpha" value="0.5"/>
```

Here, *target* specifies the object containing the property to change, *name* is the property whose value needs to be changed and *value* is the new value for the property.

### 6.2.2.3 The <mx:setStyle> tag

The <mx:setStyle> tag is used to set the value of some style that will hold only for a particular view state:

```xml
<mx:SetStyle target="(this)" name="backgroundColor" value="#ffcccc"/>
```

Here *target* specifies the object whose style is to be changed, *name* is the style that needs to be changed and *value* is the new value for the style.

## 6.2.3 Adding components

Not only the behavior or look and feel of an existing component can be changed during a state, but also new components can be added or existing components can be removed. This is done as defined below.

### 6.2.3.1 The <mx:AddChild> tag

This tag tells Flex that when the application is in this state, a child needs to be added. The child can be any component such as a button or textarea. *Listing 6.3* shows an example of using this tag.

```xml
<mx:AddChild relativeTo="(panel1)" position="lastChild"
          creationPolicy="all">
      <mx:TextArea id="t1" text="New State"/>
</mx:AddChild>
```

and the `none` value means that the child will not be created until a method, `createInstance()` is called to create it.

### 6.2.3.2 The <mx:RemoveChild> tag

This tag tells Flex that when the application is in this state, a child needs to be removed.
The child can be any component such as a button or TextArea.

```xml
<mx:RemoveChild target="{linkButton1}"/>
```

# 6.3 Behaviors

An *effect* is some visible change to a component that operates over a predetermined duration which is measured in milliseconds. Examples of Flex effects include `wipedown` effect, `blur` effect, `dissolve` effect etc. A *trigger* is an action such as a mouse click.
However, it should not be confused with an event. A trigger causes an effect to occur and an event makes a call to an Actionscript function or object. For example, a component can have a `focusOut` event and a `FocusOutEffect` trigger. An effect when registered with a trigger creates a *behavior*. A behavior lets you add motion, sound and animation to the application.

## 6.3.1 Common Effects

*Table 6.7* lists the effects that Flex supports.

| Effect | Description |
|---|---|
| AnimateProperty | Used to animate a numeric property of a component, such as height, width, scaleX, or scaleY. |
| Blur | Used to apply a blur visual effect to a component. |
| Dissolve | Used for modifying the alpha property of an overlay to gradually have to target component appear or disappear. |
| Fade | Used to animate a component from transparent to opaque, or from opaque to transparent. |
| Glow | To apply a glow visual effect to a component. |
| Iris | Used to animate the effect target by expanding or contracting a rectangular mask centered on the target. |
| Move | Used to change the position of a component over a specified time interval. |
| Pause | Does nothing for a given period of time. |
| Resize | Changes the width and height of a component over a specified time frame. |
| Rotate | Rotates a component around a specific point. |
| SoundEffect | Used to play an MP3 audio file. |
| WipeLeft, WipeRight, WipeUp, WipeDown | Used to define a bar Wipe effect. |
| Zoom | Used to zoom a component in or out from its center point. |

Table 6.7 - Common Effects

## 6.3.2 Using Effects

You can alter how to play effects by calling the pause(), resume(), or end() methods. The pause() method pauses an effect, the resume() method allows you to resume a paused effect and the end() method ends an effect that is being played.

When an effect starts, a startEffect event is dispatched and when it ends, an endEffect event is dispatched. You can use these events and perform specific functions if required.

Effects can be played in sequence or parallel using the <mx:sequence> and <mx:parallel> tags respectively. Effects defined in a sequence are played one after the other and those defined in parallel are played at the same time.

You will get a better idea about using effects with an example. So let us create an image that blurs when a user clicks it. Follow these steps:

- 1. Create a new Flex project.
- 2. Add an images folder in the src folder and add an image in this folder. For this example we have an image named rambutan.jpg that is included in the accompanying zip file (Exercise_Files_AdobeFlex.zip) under sub-directory Chapter 6.
- 3. Go to the design view. Drag and drop a panel and add an image on the panel. You can choose the properties for the panel, or use the ones shown in Listing 6.4 below.

```xml
<mx:Panel title="Blur Effect" layout="vertical" color="0xffffff"
borderAlpha="0.15" width="500" paddingTop="10" paddingRight="10"
paddingBottom="10" paddingLeft="10" horizontalAlign="center">
<mx:Image id="fruit"
source="@Embed(\"/assets/images/fruit.jpg\")"/>
</mx:Panel>
```

Listing 6.4: Adding Panel to the application

- 4. Now you can define the Blur effect along with its properties as shown in Listing 6.5 below.

```xml
<mx:Blur id="blurImage" duration="1000"
blurXFrom="0.0" blurXTo="10.0"
blurYFrom="0.0" blurYTo="10.0"/>
<mx:Blur id="unblurImage" duration="1000"
blurXFrom="10.0" blurXTo="0.0"
blurYFrom="10.0" blurYTo="0.0"/>
```

Listing 6.5 - Defining a blur effect

- 5. Now you need to define the `trigger` that initiates the effect. The `id` property of the effect specifies which effect is played when the trigger occurs.

```xml
<mx:Image id="fruit" source="@Embed('images/fruit.jpg')"
mouseDownEffect="{blurImage}" mouseUpEffect="{unblurImage}"/>
```

- 6. Go ahead and run this application. You can see in *Figure 6.7* how nicely the image blurs and then comes back to the initial state upon being clicked.

![](img/c4119654311ebf24679359ca130a5ee6_123_0.png)

## 6.3.3 Customizing Effects

Effects are customized by specifying effect properties in the code. For example, in the above sample application, the `duration` property defined how long the blur lasts in milliseconds.

```xml
<mx:Blur id="blurImage" duration="1000" blurXFrom="0.0" blurXTo="10.0"
blurYFrom="0.0" blurYTo="10.0"/>
```

## 6.4 Transitions

A transition is a way to turn a state on or off in a graceful manner. Transitions are actually effects that are grouped together and played whenever a state change happens. Transitions apply their effects to one or more components. Like the `states` property of a component, the `transitions` property is also inherited from the `UIComponent` class.

### 6.4.1 Making states more interesting

Transitions and states are very much interrelated. The State class defines all the actions that will change from the base state. This includes adding or removing components from the base view state, setting properties, setting styles or setting event handlers. In the transitions class you define the order of all of those actions. The changes that occur in the state are declared again in the transitions definition. If you do not apply a transition to a state, the changes of that state are applied instantly and no transition occurs.

You can have different transitions from different states. The `<mx:transitions>` tag defines an array of transition objects. The `<mx:Transition>` tag defines a transition. It has the toState and fromState properties, which specify the states to which the transition has to be applied. By default, both the fromState and toState properties are set to "*", i.e., apply the transition from any state to any state. The fromState property specifies the view state that you are changing from, and the toState property specifies the view state that you are changing to. With transitions you can specify to apply the changes in Parallel or Sequence order. The syntax is:

```xml
<mx:Transition id="ID" fromState="*" toState="*" />
```

### 6.4.2 Using Action Effects

Flex defines several action effects to control the order of view state changes when a transition takes place. When a view state is created, there are four classes that are used to define the view state. Each of these classes has a corresponding action effect that is used to control when a change, defined by the view state property occurs in a transition.

Table 6.2 describes the action effects

| Action Effect | Corresponding view state Class | Use |
| :--- | :--- | :--- |
| SetPropertyAction | SetProperty | Used to set a property value as part of a transition. |
| SetStyleAction | SetStyle | Used to set a style to a value as part of a transition. |
| AddChildAction | AddChild | Used to add a child as part of a transition. |
| RemoveChildAction | RemoveChild | Used to remove a child as part of a transition. |

Table 6.2 - Action Effects

Let us now add some transitions to the previous example on States to see how it works.
