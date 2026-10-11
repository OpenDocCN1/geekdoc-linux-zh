
## FOSS Picks

Sparkling gems and new releases from the world of Free and Open Source Software

![](img/8286bf901ba268fe114d66ada92d1dd6_79_0.png)

Graham had an interesting moral dilemma this month: whether to include an open source Wordle clone or not. Read on to see his decision.

BY GRAHAM MORRISON

### Graphics studio

#### Blender 3.0

We've looked at updates to Blender before but never one as significant as this. Blender 3.0 comes 22 years after Blender 2.0. This period covers the project from directly after the source code was released as freeware in 2000 through the creation of the Blender Foundation in 2002 and its true open sourcing in 2003, before the incredible number of world-changing feature updates that have defined the 2.x release cycle. Hugely influential, Blender is a lightweight project for what open source can achieve. From modeling, animation, movies, and 3D rendering to architecture, 3D printing, and game design, Blender has received unparalleled industry recognition and is used by hobbyists, students, and professionals alike.

Not just a token release, Blender 3.0 contains a significant number of new features and refinements, especially if you've skipped a few updates. The best of these is the asset browser, a new kind of view type that appears in the menu alongside the 3D viewport, compositor, and all the other types. When enabled, the chosen pane will show thumbnails from a huge number of Blender asset types, including objects, materials, and even poses. Poses are a way of storing character expressions for your models, such as a smile or frown. Blender 3.0 will let you tweak these poses without losing the original, with keying sets for both characters and properties. You can then add, blend, apply, and flip poses from the asset view to see how they'll fit on your chosen character. Key values can even be selected by dragging a square across the frame graph.

Equally, assets can be dragged and dropped into your scene, which will update as quickly as your hardware allows, even when adding high-dynamic range image (HDRI) lighting assets. It's a great way to quickly drag a model with materials and lighting into your scene. You can contribute back to the library by marking scene elements as assets – which can also be linked, rather than copied – so that only a single instance is used across multiple projects.

Speed and quality improvements are everywhere. The knife tool can cut across multiple objects and is finally included in the undo history. Drawing strokes can be modified concurrently, and six degrees of freedom (6DOF) controllers have even been added to the virtual reality mode. When you generate final output, rendering is two to eight times faster thanks to the new Cycles X renderer. Viewport updates are faster, as is point-of-view (POV) mode for setting up a camera, which even in complex scenes remains interactive enough to line up shots, with further detail added the longer that view is maintained. Everything looks better, with improved shadows, hardware ray tracing, and light scattering on the surface of materials. Even the UI is much improved. If you've not used Blender for a few years, you'll find on-screen prompts, sliders, and controls are now available for almost every function. Each view is accompanied by icons or glyphs for the main functions, and everything is a lot more intuitive than it used to be. There are still many options and many menus, but you can get started without using 90 percent of them. This is helped by the default theme which now has more configurable contrast and even more rounded corners. Blender is now easier to use than ever and even more capable of producing amazing results.

![](img/8286bf901ba268fe114d66ada92d1dd6_79_1.png)

- **Viewport rendering:** The previewed output in Blender now looks almost identical to the final output.
- **UI improvements:** Mouse over an area to highlight its edges and more easily join or merge different panes.
- **Geometry nodes:** This release has new nodes for interaction with curves, text data, and instances.
- **Properties display:** Rather than guessing or remembering key combinations, properties can be changed with the UI in the viewport.
- **Improved icons:** Glyphs and icons across Blender are now much easier to understand and use.
- **Speed improvements:** Not just in the preview – everything is now faster, from nodes to rendering.
- **Asset manager:** Keep all your best ideas in one place across projects, including character poses.

### Project Website

https://www.blender.org

### Console web service access

#### woob

**Wo**ob is an acronym for “web outside of browsers”, and its mission is to provide access to specific websites without requiring a web browser. It does this by being a module-driven back end, with each module targeting a specific kind of web service. Type `woob` followed by `bank`, for example, and you’re presented with a huge list of modules designed to work with online banks. What’s most surprising is that while the project is young and relatively niche, there’s already a huge number of modules to support each of its capabilities, with more being added all the time. There’s support for 88 banks, for example, from Barclays to Swiss Life. Selecting one of these will walk you through configuring the module with your own credentials so you can access whatever capabilities the module supports. For the bank module, these capabilities include viewing your interest rate, the ability to transfer funds, and retrieving your balance. Of course, you might wisely not trust woob to negotiate your bank account without some kind of audit of its code, but woob also supports many less crucial services. The cinema capability lets you interact with film metadata grabbers and local download services. The gallery module does the same for picture services, while parcel helps you access tracking information from companies such as DHL and DPD. There are many more, including those that deal with local Linux command-line tools and sensors, remote web services such as weather and bug tracking, and even cooking recipes and music lyrics. You don’t even need to use the command line because many are accompanied by a Qt-based graphical front end, which can be used instead of the command line. These have the added advantage of showing images such as movie posters, album covers, or recipe photographs. It can take some effort to get started, but after you’ve used a couple of modules you realize it offers a better user experience than many of the web services it hopes to replace, and that’s definitely a good thing.

![](img/8286bf901ba268fe114d66ada92d1dd6_80_0.png)

Access some of your favorite web services from the command line – without a web browser – with woob.

### Project Website

https://woob.tech

### Cat clone

#### bat

**The** Unix philosophy of having one simple tool to do one simple task is still alive and well on the command line, and the `cat` command is one of its best examples. It’s a command so venerable that it was included in the original first edition of “Research Unix,” developed by Ken Thompson and Dennis Ritchie in 1971 (though the term “Research Unix” was first used in 1978). As everyone knows, `cat` will print the contents of a text file to the standard command-line output, letting you easily see its contents. If more than one file is listed, it will concatenate the output of each in turn (the task that gives it its name) and let you view its contents as a whole or pipe them back into a new, single file. It can optionally display line numbers, or highlight tabs or the end of a line, but it can’t do much more. It’s a simple tool for a simple job, and it works brilliantly.

But there are times when you sometimes need a little more from the humble `cat`, especially when rummaging through source code or text files with a specific format. This is where the equally zoomorphic bat can help. It extends `cat`’s simple premise with a few extra modern essentials, including syntax highlighting, built-in paging, and even `git` integration that can show only the modifications in a file after comparing it with the Git index. All of this happens when you simply replace your `cat` invocation with `bat`, but there are further options to customize the output too, including options to specify when to disable the pager, when to display only the differences, and the one file type maps to another. It’s fast, looks beautiful, and can be themed, while still remaining completely compatible with `cat`’s original basic output, making it just as useful for previewing `fzf` or finding results as it is previewing the contents of `main.cpp`.

![](img/8286bf901ba268fe114d66ada92d1dd6_80_1.png)

bat is one of those rare commands that makes you wonder how you ever lived without after you start using it.

### Project Website

https://github.com/sharkdp/bat
