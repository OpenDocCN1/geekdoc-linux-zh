The purpose of the `<div>` tag is to define an area on the page that is used for a specific purpose. The `<div>` areas specify not only major areas, such as headers or sidebars, but also smaller areas, such as box-outs (separate boxes filled with information) that contain additional information. Inside the `<div>` and `</div>` tags, the relevant code for that area is added.

It is important that the `<div>` areas are added in the same order as the page flows. If for some reason the CSS file is unavailable, the correct ordering of the `<div>` areas still provides the correct page structure, albeit without any design. This is particularly important for supporting devices, such as phones and PDAs, that do not have full support for CSS.

For example, if you want to include a header area, a main content area, and a footer area, you could use the following `<div>` tags (note that order matters here):

```
<div id="header"> </div>
<div id="main"> </div>
<div id="footer"> </div>
```

When creating `<div>` tags, you can name them with the **id** or **class** attributes. Although both of these two attributes reference the `<div>` area from the stylesheet to style them, **id** and **class** have different purposes. If you use the **id** attribute, you can use only one `<div>` by name on the page. If you use the **class** attribute, you can use more than one `<div>` by that name on the page. As such, use the **id** attribute for major areas, such as the header, main section, and footer, and use the **class** attribute for page "furniture" (the different parts of a page), such as box-outs, which could appear multiple times.

The first step, before you even think about creating any code, is to get an idea of how your page will be *structured*. Start by knowing the basic sections of your pages. If you look at Figure A-3, you can see several distinct areas:

+   - At the top of the page is a consistent gray area that contains the name of the site.
+   - Below the top area is a menu bar.
+   - A gray sidebar is on the left side of the page. This area is useful for information relevant to the main content.
+   - The main body of the page is where the content will be displayed.