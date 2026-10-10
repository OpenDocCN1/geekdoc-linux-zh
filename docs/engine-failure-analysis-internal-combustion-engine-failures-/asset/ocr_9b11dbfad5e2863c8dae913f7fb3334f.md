**75DPI AND 100DPI PROPORTIONALLY SPACED (SCALABLE) (CONT.)**

| adobe | new century schoolbook | medium | italic | normal | | iso8859-1 |

| adobe | symbol | medium | roman | normal | | adobe-font-specific |

| adobe | times | bold | roman | normal | | iso8859-1 |

| adobe | times | medium | italic | normal | | iso8859-1 |

| adobe | utopia | regular | italic | normal | | iso8859-1 |

| adobe | utopia | regular | roman | normal | | iso8859-1 |

| b&n | lucida | bold | italic | normal | sans | iso8859-1 |

| b&n | lucida | bold | roman | normal | sans | iso8859-1 |

| b&n | lucida | medium | italic | normal | sans | iso8859-1 |

| b&n | lucida | medium | roman | normal | sans | iso8859-1 |

| b&n | lucidabright | demibold | italic | normal | | iso8859-1 |

| b&n | lucidabright | demibold | roman | normal | | iso8859-1 |

| b&n | lucidabright | medium | italic | normal | | iso8859-1 |

| b&n | lucidabright | medium | roman | normal | | iso8859-1 |

| bitstream | charter | medium | italic | normal | | iso8859-1 |

| bitstream | charter | medium | roman | normal | | iso8859-1 |

# Font Configuration Files

In order to make fonts available to the X server, a directory must contain, minimally, a **fonts.dir** file created with **mkfontdir**. For scalable fonts, the directory must also contain **fonts.scale**. This file is referenced by **mkfontdir**, so it must be created before the **fonts.dir** file. If the fonts contain an encoding that the X server does not recognize by default, you must create the **fonts.dir** file with **mkfontdir -e**, which creates the **fonts.encoding** file. You can also create a **fonts.alias** file so that you can refer to the fonts using a shorter name.

You must also configure the X server by indicating the location of the directories containing fonts. With XFree86, this information is contained in the XF86Config file (in the /etc directory on most systems)