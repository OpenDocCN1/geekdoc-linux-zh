The second step uses the $Style argument to construct the object, with sizes:

```
switch($style) {
    case STYLE_TABLET_LARGE:
        return new WebBrowser(new WAM_FactoryTouch($style), 1024, 740);

    case STYLE_TABLET_SMALL:
        return new WebBrowser(new WAM_FactoryTouch($style), 480, 320);

    case STYLE_FULL:
    default:
        return new WebBrowser(new WAM_Factory(STYLE_FULL));
}
```

In each case, the WAM_Factor* class indicates which applet manager to create is currently either Warp_Applet_Manager or Warp_Applet_ManagerTouch, the latter uses large clickable icons rather than small icon and text for its interface.

Instead of using a single page containg all the applets, you can produce several pages and use the main applet to switch between them. This is shown in its maximized view in Figure 7-3.

![](bbox=[0.066, 0.395, 0.801, 0.719])

*Figure 7-3.* The main applet

The main applet has two functions. The first is to enumerate each applet added into the applet manager on that page, thus providing similar functionality to the minimized boxes on the right but with larger graphics (that is, better