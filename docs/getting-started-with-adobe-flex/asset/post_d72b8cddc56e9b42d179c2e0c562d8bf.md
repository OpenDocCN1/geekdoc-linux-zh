
## 4.3 Containers

Flex containers can be broadly classified into three types: Application, layout, and navigation. Each type is explained in the following section with specific examples.

### 4.3.1 Application containers

An application container is the default container for any Flex content or component – as soon as you create a new *Application*, this container is created.

In the Flex perspective of Eclipse, select an existing Flex project or create a new one. Right click on that project, and choose *New* -> *MXML application*. A small window will appear. Enter in the *Filename* field the name of the application. Call it *FlexComponent*. The view shown in *Figure 4.5* is displayed.

![](img/c4119654311ebf24679359ca130a5ee6_78_0.png)

If you click on the source view, the generated code shown in *Listing 4.1* is displayed.

```xml
<?xml version="1.0" encoding="utf-8"?>
<mx:Application xmlns:mx="http://www.adobe.com/2006/mxml"
	layout="absolute">
</mx:Application>
```

**Listing 4.1** – Default generated code when you define an application

Though you can build your application using only an application container, it’s not a good practice to do so. You should place other suitable containers before using any controls in your application.

By default, the size of the application container is the size of the browser. You can change relative size of the application by specifying height & width properties; this way the application will resize itself proportionately to the browser size.

There are few important style properties for the application container:

- * backgroundColor: This color is visible during application loading and initialization
- * backgroundGradientAlphas: controls the opaqueness of the background
- * backgroundGradientColors: It changes colors from first to second; from top to bottom gradually as given in [Top color, Bottom Color]
- * backgroundImage: Image for the application background

You should paint a panel or form container in the application container before starting to add controls. For example, the code in *Listing 4.2* will put a panel for the company website you're going to build.

```xml
<mx:Application xmlns:mx="http://www.adobe.com/2006/mxml" width="100%"
height="100%">
<mx:Panel title="My Company's Web site" width="100%" height="100%"
fontSize="30">
</mx:Panel>
</mx:Application>
```

**Listing 4.2** – Defining a panel container inside an application

Run the program and you'll see the output shown in *Figure 4.6*:

![](img/c4119654311ebf24679359ca130a5ee6_79_0.png)

**Figure 4.6** – Output of the sample application

Some other characteristics of an application container are:

- For each application container defined by the `<mx:Application>` tag, there is an application object associated with it. The application object can be referred using mx.core.Application.application from anywhere in the Flex application.
- The Application class supports a preloader that uses a download progress bar to show the download progress of an application SWF file. This is discussed in more detail in the exercise section.

### 4.3.2 Layout containers

A layout container is a rectangular area rendered on the Flash Player during runtime of a Flex application. It controls the size and position of the child container and controls painted within it. You can think of layout containers as place holders for other controls and containers. *Table 4.1* lists the layout containers in Flex 3.0.

| Container Name | Usage/Description |
|---|---|
| Canvas | Rectangular region which needs specific positioning (non- automatic) of child components |
| Box | Rectangular layouts where components are placed either horizontally or vertically |
| HBox | |
| VBox | |
| ControlBar | Container used in Panel or TileWindow which holds components shared with other children in parent component |
| ApplicationControlBar | Container holds components which provides access to application navigation controls |
| DividedBox | |
| HDividedBox | |
| VDividedBox | |
| Form | Form is the most commonly used container which allows validation, data binding and usage of style sheets. FormHeading is an optional heading group of FormItem Components. FormItem is a specific form element with a single label and one or more child components |
| FormHeading | |
| FormItem | |
| Grid | Grid layout container arranges its child components as rows and columns – similar to an HTML table |
| Panel | Panel layout container consists of title bar, title, a border, content area and a status area |
| Tile | Tile layout container which lays out child components in horizontal or vertical alignments. All containing cells are of same size. |
| TileWindow | TileWindow layout container optimized for usage as pop-up window |

**Table 4.1** – Layout containers in Flex

**Note:**
In the above and following tables, there are some containers that do not have an icon associated to it. For example, Box – Usually they are by default replaced by one if the sub-classes (e.g. HBox in this case). In some cases, few controls can only be rendered by ActionScript – no MXML equivalent like Menu. In summary, you can’t drag and drop those controls – you can create them using ActionScript only.

### 4.3.3 Navigation containers

Navigation containers hold other containers so that you can navigate among its children.
*Table 4.2* contains the list of Navigation containers in Flex 3.

| Container Name | Usage/Description |
|---|---|
| ViewStack | This container is made of a collection of child containers which are stacked on top of each other. Only one child can be visible or active at a time. |
| TabNavigator | This container creates, holds and manages a set of tabs — each tab in turn can hold other containers. |
| Accordion | This container defines and holds a set of child active containers where only one container is fully visible at a time |

**Table 4.2** – Navigation containers in Flex

The following section will show you some examples of the above containers. For illustration purposes, we will use some controls which are described in the next sections.

To see some of the above containers in action, let’s continue with the earlier example:

1. Select a HDividedBox container and put it inside the Application container.
2. Put an Accordion container on the left hand side.
3. Place a TabNavigator container on the right hand side of the HDividedBox container.
4. Draw three Canvas containers inside the TabNavigator container.

We’ll adjust some simple properties for the containers to fit them nicely on the screen starting from the generated MXML code shown in *Listing 4.3* below.

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

**Listing 4.3** – code for sample navigation containers

The output of the code is shown below:

![](img/c4119654311ebf24679359ca130a5ee6_82_0.png)

**Figure 4.7** – Sample application output with layout containers

You can see that it's very easy to build a decent looking Web page with little code and very little time. You can change the size of the left and right pane of the HDividedBox – also you can navigate different canvases inside the Accordion or TabNavigator.

## 4.4 Controls

Controls are the Flex user interface components with which users interact. Controls are always placed inside containers. All controls like containers are created as a derived class of *mx.core.UIComponent* as shown in **Figure 4.8** below.

![](img/c4119654311ebf24679359ca130a5ee6_82_1.png)

**Figure 4.8** – Class hierarchy of Button and Level controls

Based on property and usage, Flex controls can be broadly divided into four categories which are described in the following sections.

### 4.4.1 Text-based controls

Use these controls to display and edit text and related details in your Flex application. All controls except *RichTextEditor* are simple controls. *RichTextEditor* has more than one control (TextArea, ControlBar and few other formatting ones) as part of it. **Table 4.7** lists the Text-based controls in Flex 3.
