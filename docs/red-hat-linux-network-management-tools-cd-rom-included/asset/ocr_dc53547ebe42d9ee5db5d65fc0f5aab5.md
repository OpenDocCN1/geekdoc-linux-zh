WAN. Therefore, import the background image called `usa-image.xbm`.

+   4. Create devices that are used to support the WAN. This includes routers, modems, and any other associated devices. For our example, a total of four routers have been added to the view: `wan-remote.home.com`, `fi-gw.home.com`, `tx-gw.home.com`, and `ca-gw.home.com`.

+   5. Create connectivity objects between each of the routers showing the correct topology of the network.

+   6. Add a descriptive label using the Text tool.

+   7. Now that you have completed this view, you should make a link from the first view (*top-level* view) to the *WAN-view*. You can do this by creating a reference object on the *top-level* view. To add this object to the view, select the reference icon with the left mouse button. Next, left-click on the topology map where the object should be placed.

+   8. Once you create the reference object, you must add it to the *WAN-view*. To do this, right-click on the reference object to display the dialog box shown in Figure 11.21. Enter the name *WAN-view* in the name field to serve as the name of the object. Next, specify the full pathname and filename of the file that contains the *WAN-view* topology map. In this example, the path and file is `/home/network-views/WAN-view`. Click the *Set Value* button to save this information.

![](bbox=[0.18, 0.7, 0.8, 0.82])

**Figure 11.21** Reference object attributes dialog window.