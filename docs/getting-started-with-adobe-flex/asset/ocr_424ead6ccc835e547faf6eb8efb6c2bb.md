# 6.2.1.1 The <mx:states> tag

The states property defines an array of view states for a view component. Every view component will have a base state, which is the first state. The base state is the default state of any Flex application. The states property cannot be specified on any child controls. It can only be specified on the root of a custom control or application.

# 6.2.1.2 The <mx:State> tag

A State object can be added to the state property of the component. Adding so, will create new view states for that component.

Syntax of the <mx:State> tag:

```
`<mx:State basedOn="null" name="null" overrides="null"/>`
```

The basedOn attribute specifies the view state on which it is based on and the name attribute specifies the name of the current State object. The purpose of a state is to alter the appearance of a component in response to a user or system-initiated event, for example, the click of a button. Altering the appearance of a component involves the use of overrides via a state. Valid overrides include:

+   * AddChild
+   * RemoveChild
+   * SetEventHandler
+   * SetProperty
+   * SetStyle

# 6.2.2 State properties, style and events

In order to further customize a state in terms of look and feel and behavior, the following tags can be used.

# 6.2.2.1 The <mx:SetEventHandler> tag

The <mx:SetEventHandler> tag allows you to create event listeners that are active only during a specific state. This is made possible by using the handler event type or the handlerFunction property.

In the handler event type, you can specify more than one parameter for the event listener function. You can even add ActionScript code within the tag instead of providing an event listener function. This is shown in the example below:

```
<mx:SetEventHandler target="(Button)" name="ButtonClick"
    handler = "buttonHandler(event, linkButtonID)"/>
```