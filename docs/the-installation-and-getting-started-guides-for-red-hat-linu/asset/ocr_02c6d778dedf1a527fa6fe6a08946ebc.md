set to use GMT/UTC, add the --utc option to your timezone line. Here's an example that defines the timezone as US Eastern with the system clock set to GMT:

```
timezone --utc
US/Eastern
```

# xconfig — X Window Setup

The next item is the X Window setup line. The installation program will normally find common PCI video hardware and will know which X server to install. The keyword for X configuration is xconfig. If your video card isn't autoprobed properly, you can use the --card option to explicitly specify the card. You can use Xconfigurator --help on a running Red Hat Linux system to get a list of supported cards to choose from. If your card isn't in the list but is supported by one of the existing servers, you can simply install the proper server by using the --server option. Again, use Xconfigurator --help to get the list of server names. You also need to specify a monitor type. If you don't, the installation will assume a generic monitor capable of 640x480@60hz. Use the --monitor option to specify something other than the default. Again, Xconfigurator --help will list all valid monitor types. If your monitor isn't listed, you can enter the actual monitor specifications by using the --hsync and --vsync options for horizontal and vertical sync rates, respectively. The rates may be single numbers (representing kilohertz and megahertz, as appropriate), groups of numbers separated by commas, or two numbers separated by a dash (signifying a range). For example:

```
xconfig --hsync "31.5,35.5,50-65" --vsync "50-70"
```

An example for a machine where the video card can be autoprobed properly would be:

```
xconfig --monitor "tatung cm14uhe"
```

An example for a machine where nothing is probed and the monitor