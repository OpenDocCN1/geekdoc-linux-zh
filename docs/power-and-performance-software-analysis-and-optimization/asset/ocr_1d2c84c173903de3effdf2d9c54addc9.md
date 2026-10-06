# 7.2 Data collection and reporting 131

On the other hand, Listing 7.4 illustrates the same data and report, but grouped by source code line.

```
$ amplxe-cl -report hotspots -result-dir r000ge | head -n 15
Function Module CPU Time:Self
def defate_quick minigzip 5.708
compare258 minigzip 5.442
quick_insert_string minigzip 5.055
quick_send_bits minigzip 2.635
quick_send_bits minigzip 1.548
[vlinux] vmlinux 1.525
crc_fold_copy minigzip 1.293
static_emit_ptr minigzip 1.171
quick_send_bits minigzip 1.075
fill_window_sse minigzip 0.992
_mm_subs_epul6 minigzip 0.658
static_emit_lit minigzip 0.494
```

# LISTING 7.3

Excerpt of hotspots report of General Exploration analysis.

```
$ amplxe-cl -report hotspots -result-dir r000ge -group-by=source-line
Source Line Module CPU Time:Self
deflate_quick.c 31 minigzip 5.399
deflate_quick.c 155 minigzip 4.592
deflate_quick.c 182 minigzip 1.613
[Unknown source file] [Unknown] vmlinux 1.525
emminintrin.h 702 minigzip 1.128
deflate_quick.c 95 minigzip 0.986
deflate_quick.c 183 minigzip 0.946
deflate_quick.c 86 minigzip 0.907
deflate_quick.c 104 minigzip 0.866
emminintrin.h 1081 minigzip 0.747
deflate_quick.c 94 minigzip 0.584
deflate_quick.c 189 minigzip 0.554
```

# LISTING 7.4

Excerpt of source grouped hotspots report of General Exploration analysis.

# Graphical interface

In general, the graphical interface is very flexible, with formatting options depending on the data collected, the viewpoint, and many other configurable options. As a result, it is not productive to attempt to document all of these interfaces and means. This section attempts to highlight some important points and explain the general concepts. If more detail is required, check the VTune documentation or contact Intel support.