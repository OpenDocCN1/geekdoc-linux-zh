![](bbox=[0.16, 0.165, 0.84, 0.205])

In the figure, *View State 1* is the initial state of the UI. When the defined *transition* is applied to this view state the UI changes to *View State 2*. A transition is defined using different effects (*Effect 1, Effect 2... Effect N*). These effects can be applied conditionally using different *filters* along with effects. Filters are used to conditionally apply the defined effects only on a subset of target components defined in the *transition*.

# 6.2 View states

*States* are a collection of changes to a view. Let us say that we have a view with many components (containers and controls). Then, if any change occurs to the layout of any of these view components, then it becomes a view state. Every component that inherits the `UIComponent` class will have view states and these components will inherit the states property.

# 6.2.1 Creating States

States can be easily created in Flex Builder using the design view. Let us see how this can be done using a simple example. Follow these steps:

+   1. Create a new Flex project.

+   2. Switch to design view and using the layout tools, add two components, a panel and a button as shown in *Figure 6.2* below. This now becomes the base state of the application.

![](bbox=[0.22, 0.565, 0.62, 0.675])

+   3. Now you can create a new state based on this base state. Select *Window -> Show View -> States* to open the States view. *Figure 6.3* shows the States view. Now click on the *New State* icon as shown in the below figure. A popup window appears. Name the new state as *firstState* and then specify the component on which it is based. In this example it is based on the `<base state>`. You can optionally tick the ‘set as Start state’ option if this state should be the start state. Leave that option un-ticked for the time being since we want the base state as the start state.