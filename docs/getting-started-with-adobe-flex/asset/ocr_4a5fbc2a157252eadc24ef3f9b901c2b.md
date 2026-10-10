![](bbox=[0.15, 0.15, 0.45, 0.3])

Figure 5.2 - List Control

# 5.4.1.2 HorizontalList control

The HorizontalList control displays a horizontal list of items. It is particularly useful for displaying a list of images. The `mx.controls.HorizontalList` class can be used in a Flex application by using the `<mx:HorizontalList />` MXML tag. Listing 5.16 provides a code snippet example that uses the `<mx:HorizontalList/>` MXML tag. Figure 5.3 illustrates how the HorizontalList would look.

```
`<mx:HorizontalList id="myList" width="200" height="50" dataProvider="{shapes}"/>`
```

Listing 5.16 - Code Snippet to create a HorizontalList control

![](bbox=[0.15, 0.52, 0.45, 0.65])

Figure 5.3 - HorizontalList Control

# 5.4.1.3 TileList control

The TileList control is similar to the List and HorizontalList controls as discussed earlier except that it displays the item in a tile-like fashion and the direction of the layout can be specified. The height and width of the individual tiles can also be set by setting the width of the Tilelist columns or the height of the TileList rows. The `mx.controls.TileList` class can be used in a Flex application by using the `<mx:TileList />` MXML tag. Listing 5.17 provides a code snippet example and Figure 5.4 illustrates how the horizontal TileList would look.

```
`<mx:TileList direction="horizontal" dataProvider="{shapes}" rowCount="2" rowHeight="100"/>`
```

Listing 5.17 - Horizontal TileList in MXML