| TabNavigator■■■ | This container creates, holds and manages a set of tabs — each tab in turn can hold other containers. |
|---|---|
| Accordion■■■ | This container defines and holds a set of child active containers where only one container is fully visible at a time |

# **Table 2.2 — Navigation containers in Flex**

The following section will show you some of examples of the above containers. For illustration purposes, we will use some controls which are described in the next sections.

To see some of the above containers in action, let’s continue with the earlier example:

+   1. Select a HDividedBox container and put it inside the Application container.
+   2. Put an Accordion container on the left hand side.
+   3. Place a TabNavigator container on the right hand side of the HDividedBox container.
+   4. Draw three Canvas containers inside the TabNavigator container.

We’ll adjust some simple properties for the containers to fit them nicely on the screen starting from the generated MXML code shown in *Listing 4.3* below.

```
```xml
<?xml version="1.0"?>
<!-- containers\application\AppSizePercent.mxml -->
<mx:Application xmlns:mx="http://www.adobe.com/2006/mxml" width="100%"
height="100%">
<mx:Panel title="My Company's Web site" width="100%" height="100%"
fontSize="30">
<mx:HDividedBox width="100%" height="95%">
<mx:Accordion x="40" y="32" width="15%" height="100%"
maxWidth="300">
<mx:Canvas label="Accordion Pane 1" width="100%" height="100%">
</mx:Canvas>
</mx:Accordion>
<mx:TabNavigator width="85%" height="100%">
<mx:Canvas label="Tab 1" width="100%" height="100%">
</mx:Canvas>
<mx:Canvas label="Tab 2" width="100%" height="100%">
</mx:Canvas>
</mx:TabNavigator>
</mx:HDividedBox>
</mx:Panel>
</mx:Application>
```
```

# **Listing 4.3 — code for sample navigation containers**

The output of the code is shown below: