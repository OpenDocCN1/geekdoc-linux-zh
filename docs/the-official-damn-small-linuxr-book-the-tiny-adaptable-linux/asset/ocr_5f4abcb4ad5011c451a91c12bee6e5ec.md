![](bbox=[0.15, 0.15, 0.85, 0.52])

FIGURE 2-4 Press F3 to view boot options for setting passwords, choosing a desktop, or setting other boot time features.

# Trying Different Boot Options

Let's roll up our sleeves, try some common boot options, and discuss some common solutions. At the boot prompt, let's try a few basic options.

+   Video boot options—By default, DSL boots into a high resolution, vga=791 mode. This might be too high a resolution for your computer's video. Using the boot option vga=normal might help.

```
boot: dsl vga=normal
```

Many older laptop/notebook computers require framebuffer video instead of the Xvesa. So, you might want to try:

```
boot: fb800x600
```

Note that I did not use the word dsl as the first option. Depending on your notebook computer, it might be fb1024x786. If you get an error about no fbdev, using framebuffer likely will not help.

Notice the vga resolution table on the F3 screen (see Figure 2-4). Any one of these values can be selected with the vga= option.

As I noted, it can be a combination of options that is required. Try this common selection of options:

```
boot: dsl vga=normal noapic noacpi pn bios=off acpi=off noapm
```