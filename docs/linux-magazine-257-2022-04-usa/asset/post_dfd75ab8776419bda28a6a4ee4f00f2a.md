
# A plotting library

## Data Visualization

Matplotlib offers so many options that you may have trouble deciding on which ones to use for your plots. **BY MARCO FIORETTI**

Matplotlib [1] is an open source Python library for high-quality data visualization, which you can use interactively or inside scripts. While Matplotlib might look like just a supercharged version of the venerable plotting utility Gnuplot [2], that’s not the whole story. Matplotlib really shines in the integration of charting with heavy numeric processing. When combined with other Python libraries, such as NumPy and pandas (see the “Matplotlib’s Partners: NumPy and pandas” box), Matplotlib is often considered an effective and feature-rich alternative to MATLAB [3].

Some tools have steeper learning curves than others. In my opinion, Matplotlib’s learning curve is wider, not steeper than average. For example, Matplotlib has an entire tutorial devoted to colors specifications! In other words, Matplotlib has so many features and options that it looks much more complex than it actually is. For this reason, much of this tutorial uses simplified versions of some official examples to introduce the main Matplotlib concepts and features and connects the dots between them.

## NumPy and pandas

NumPy [4] is the core library for scientific computing in Python. As far as Matplotlib is concerned, NumPy’s most important components are the high-performance data structures used in some examples of this tutorial and the functions to manage them. Pandas [5] is another library, specializing in manipulation of numerical tables and time series. The combination of Matplotlib, NumPy, and pandas for numeric processing is really powerful, but it is also a relatively advanced topic that would be impossible to cover properly in just one tutorial for beginners. However, Matplotlib is really useful even alone. What you will learn with this tutorial will make it easier to add NumPy and pandas later on.

## Install Procedure

You will find several ways to install the most recent stable version of Matplotlib, all properly documented on its website. However, unless you *really* need the LATEST stable version, I strongly suggest that you save time and frustration by installing whatever binary packages are available in your preferred distribution’s official repository. On Ubuntu 21.04, for example, you can install a recent Matplotlib and all its dependencies by just searching for it in the Ubuntu Software Center or, as I did, by typing this command at the prompt:

```bash
$ sudo apt-get install python3-matplotlib
```

## Coding Styles

There are two distinct coding styles for writing and (re)using Matplotlib code: object-oriented and pyplot.

- The first style (Listing 1) uses classical object-oriented programming in any language: First you create objects (`fig` and `ax`, whose meaning I will explain shortly), and then you invoke “methods” associated to them (e.g., `ax.plot()`) to do the actual plotting.

- The second style (Listing 2) uses `pyplot` functions (in which the `plt` prefix means “use this function provided by the `pyplot` module”) to create and manage charts similar to MATLAB.

### Listing 1: Object-Oriented Style

```python
fig, ax = plt.subplots(figsize=(5, 2.7))
ax.plot(x, x, label='linear') # Create a plot
ax.legend() # Add a legend.
```

### Listing 2: Pyplot Style

```python
plt.figure(figsize=(5, 2.7))
plt.plot(x, x, label='linear')
plt.legend()
```

Listing 2, in fact, does exactly the same things as Listing 1 but by calling stateful functions such as `figure`, `plot`, or `legend` (instead of methods attached to an instance of some object). In this context, “stateful” means that each pyplot function call adds or changes something to the current state of a plot, without erasing what has been done by previous calls of other functions.

In practice, pyplot function calls have equivalent Matplotlib object-oriented methods, and vice versa, to such an extent that your choice of coding style is a matter of personal preference. However, the official Matplotlib documentation suggests using the pyplot style for “quick interactive work” and using the object-oriented style, which is more flexible, for code that will be reused often in many different ways.

# Matplotlib Terminology

Before looking at any actual code, I need to explain some basic terminology, because Matplotlib gives a few words a slightly different meaning than they have in ordinary English.

Aside from what you see on the screen, Matplotlib uses `Figure` as a keyword that creates a container of objects called “Artists.”

Basically, everything visible inside a Matplotlib Figure is an Artist, from drawings to embedded images, text captions, and so on. Each Figure keeps track of, and connects, all its child Artists, including nested subfigures, non-graphic objects such as titles or legends, and, of course, `Axes`.

An Axes (plural) is maybe the most basic and most essential Matplotlib Artist: It is a region, directly attached to a specific Figure, where you can plot some data set. You can create Axes together with their parent Figure or add them later.

Each Axes has at least a title and two labels, one per axis. Most other Artists cannot be moved to, or shared with, an Axes (that is, one specific plot or subplot) different from the one they were originally attached to.

Another essential Matplotlib term, `Axis` (singular), has pretty much the same meaning it has in normal English. An Axis object sets all the components of one axis of a plot, from the scale (linear, logarithmic, or other) to the extreme points, marks (also called ticks), and their corresponding text labels. Each Axes includes at least two Axis objects, but it is possible to add more, as shown later in this tutorial.

From figure borders to colors, there are a zillion ways to style each single detail of any Matplotlib plot and two high-level ways to set them. The quick and dirty option, which may be enough in some scenarios, is to manually set all the options you need when you generate a plot. The other option is to use full styles, which are predefined listings of all the default visual settings that your plots will need. You may load either one of the predefined styles shipped with Matplotlib using the `style.use` function:

```python
plt.style.use('somematplotlibStyle')
```

You can also load a custom style sheet from a file that you have created. In both cases, changing styles will only require you to change the one line of code that contains the style name or the path to the file that stores it. In addition, because both methods will ignore any non-visual setting that may be inside a style, styles are portable across machines with very different installations of Matplotlib.

# Data Structures

As far as data structures are concerned, no matter how you define and fill a sequence of values, Matplotlib will internally convert it to the special arrays provided by NumPy, because those are the formats that its plotting functions can handle. In most cases, you should directly use the same arrays anyway, as shown in the examples that follow, because they are faster to process than normal Python arrays and consume less memory.

# Matplotlib Gallery

With the general concepts presented above in mind, I will use some simple, but very different, examples to create plots with Matplotlib. You can easily adapt the following examples to a variety of use cases.

# A Basic Plot with Line Styling

The Matplotlib code in Listing 3 generates the plot shown in Figure 1. After loading pyplot and NumPy in the first two lines, Listing 3 defines a variable t that increases in steps of 0.2 units in the interval from 0 to 5 (line 4). Lines 6 to 8 show how to plot three different curves, each with its unique style and label. The format of the strings used to style the lines

![](img/8286bf901ba268fe114d66ada92d1dd6_88_0.png)

**Figure 1:** A really basic plot still looks nice thanks to Matplotlib styling options.
