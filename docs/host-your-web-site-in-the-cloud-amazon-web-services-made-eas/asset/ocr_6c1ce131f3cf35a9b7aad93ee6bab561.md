```
<a href="?city=Redmond&state=WA">Redmond, WA</a>
```

We also assign a special activemenu class value to the menu item if the current city matches; that way, we can add a visual style to indicate the currently viewed city in the menu.

The last element is a link to the form used to add a new classified listing. We will tackle that part of the application soon.

All that's left to do is output a list of items and format appropriately:

```
clouddlist/include/clouddlist.html.php (excerpt)
```
<div id="items">
<?php foreach ($itemCat as $category => $items): ?>
<div class="category">
<h2><?php echo $category; ?></h2>
<?php foreach ($items as $key => $attrs): ?>
<div class="item">
<h3><?php echo $attrs['Title']; ?></h3>
<?php if (isset($attrs['Thumb'])): ?>
<a href="<?php echo $attrs['Image']; ?>" target='_new' >
<img src="<?php echo $attrs['Thumb']; ?>" />
</a>
<?php endif ?>
<p class="date">Listed <?php echo $attrs['Date']; ?></p>
<p class="price">Priced at
$<?php echo number_format($attrs['Price']); ?></p>
<p class="desc">
<?php echo file_get_contents($attrs['Description']); ?>
</p>
</div>
<? endforeach ?>
<div class="clear"></div>
</div>
<? endforeach ?>

</body>
</html>
```
```

The above code uses two nested foreach loops to list all the items, categorized by their categories. The array of items is dependent on the presence of the city and