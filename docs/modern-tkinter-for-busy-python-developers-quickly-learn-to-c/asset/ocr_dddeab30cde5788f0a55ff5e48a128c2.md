Like styles, themes are identified by a name. You can obtain the names of all available themes:

```
```python
>>> s = ttk.Style()
>>> s.theme_names()
('aqua', 'step', 'clam', 'alt', 'default', 'classic')
```
```

Only one theme can ever be active at a time. To obtain the name of the theme currently in use, you can use the following:

> This API, which was originally targeted for Tk 8.6, was back-ported to Tk 8.5.9. If you're using an earlier version of Tk getting this info is a bit trickier.

```
```python
>>> s.theme_use()
'aqua'
```
```

Switching to a new theme can be done with:

```
```python
s.theme_use('themename')
```
```

What does this actually do? Obviously, it sets the current theme to the indicated theme. Doing this therefore replaces all the currently available styles with the set of styles defined by the theme. Finally, it refreshes all widgets, so that they take on the appearance described by the new theme.

# What's Inside a Style?

If all you want to do is use a style, you now know everything you need. If however, you want to create your own styles, or modify an existing one, now it gets 'interesting'.

# Elements

While each style represents a single widget, each widget is normally composed of smaller pieces, called elements. It's the job of the style author to construct the entire widget out of these smaller elements. What these elements are depends on the widget.

Here's an example of a button. It might have a border on the very outside, which is one element. Just inside that there may be a focus ring, which is normally just the background color but may be highlighted when the user tabs into the button. So that's a second element. Then there might be some spacing between that focus ring and the button's label. So that spacing would be a third element. Finally, there is the label of the button itself, a fourth element.

![](bbox=[0.16, 0.65, 0.84, 0.87])