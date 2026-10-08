# Introducing Python

# Build an app for Android with Python

# Build an app for Android with Python

Master Kivy, the excellent cross-platform application framework to make your first Android app...

![](bbox=[0.056, 0.311, 0.592, 0.473])

behaviour, the ModalView with a pop-up behaviour as used last time, and the FloatLayout as we will explain later. Kivy has many other pre-built widgets for creating GUIs, but this time we're going to focus on drawing the whole GUI from scratch using Kivy's graphics vertex instructions to create shapes (including rectangles, lines, meshes, and contextual graphics changes (such as translation, rotation, scaling, etc.), and are able to be drawn anywhere on the screen and on any widget type.

The great thing about Kivy there are loads of directions we could take it in to do some fancy things. But, we're going to make a baseline for one of Kivy's coolest features - the ability to easily run your programs on Android.

to make any sort of program you like. Once you've mastered Kivy, your imagination is the only limit. If you're pretty new to Kivy, don't worry, we won't assume that you have any pre-existing knowledge. As long as you have mastered the Python in this book so far, and have a fairly good understanding of the language, you shouldn't have any problems following along with.

We'll approach this by showing how to make a new app, this dynamic Breakout-style game. We'll then be able to compile this straight to an Android APK that you can use just like any.

Before we can do any of this we' need a class for each kind of game object, which we're going to pre-populate with some of the properties that we' need to control. Remember from last time, Kivy properties are special attributes declared at class level, which (among other things) can be modified by kv language and dispatch events when they are modified. The class will be one big widget containing

Of course, once you have mastered the basic techniques you aren't limited to using any particular kind of app, even on Android you can use all of your favourite Python libraries

Before anything else, let's throw together a basic Kivy app (Fig. 01). We've pre-implemented the widget types we'll be using, which this time are just three basic Widget with no special