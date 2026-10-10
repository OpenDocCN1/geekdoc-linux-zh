```
</mx:Script>
..
..
<mx:Canvas label="Home" width="100%" height="100%">
    <mx:LinkButton x="10" y="40" label="Company's Profile"
        textDecoration="underline" color="#636E81" fontStyle="italic"
        click="showProfile()"/>
    <mx:LinkButton x="10" y="146" label="Team's Profile"
        textDecoration="underline" color="#636E81" fontStyle="italic"/>
</mx:Canvas>
```

# **Listing 4.5 – Code for sample with basic controls**

There are 2 parts in above code listing. The top part has 2 functions,

+   * showProfile() creates TitleWindow and shows the company related text.
+   * closeMe() closes the TitleWindow.

The bottom part creates 2 LinkButton. On click of the first LinkButton, showProfile is invoked. When you run the program, you see the 2 Link buttons on the first tab as shown in *Figure 4.10*.

![](bbox=[0.17, 0.45, 0.67, 0.67])

# **Figure 4.10 – Output of the sample Basic controls**

On clicking the "Company's Profile", a title Window opens as shown in *Figure 4.11* below.