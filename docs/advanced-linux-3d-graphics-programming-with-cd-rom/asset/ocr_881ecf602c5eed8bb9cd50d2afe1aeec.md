# **Summary of Fundamental I3d Concepts**

The five-step process presented above is typical of I3d programs. First, you choose the proper fac\ntories to configure the program to its environment. Then, you declare a pipeline representing your\napplication and its data. You create an instance of the pipeline, which in turn creates screen,\nrasterizer implementation, and rasterizer objects. You “plug” this pipeline into an event dis\npatcher. Your application pipeline responds to events from the dispatcher by filling in the blanks\nleft by the virtual functions `key_event`, `update_event`, and `draw_event`. The application\npipeline draws to the screen by using the screen, rasterizer implementation, and rasterizer objects\nit created within its constructor. This forms a complete, interactive, event-driven, hardware-inde\npendent graphics program.

# **Overview of I3d Classes**

We are now ready to look at the specific I3d classes. A much more detailed development of the fol\nlowing I3d classes appears in the introductory companion book *Linux 3D Graphics Programming*.\nThe descriptions below are more of a reference, but suffice for a high-level understanding of the\nstructure of the library classes.

![](bbox=[0.15, 0.46, 0.2, 0.5])

> TIP\nAlthough the descriptions of the I3d classes presented here are not as detailed as the\nfull-blown development in the companion book, all of the sample programs and library code\nfrom the introductory companion book are also included on the CD-ROM. Therefore, you\ncan study the provided code to understand more precisely the library concepts summarized in\nthe following sections.

# **Applications and Events**

Applications written with I3d are event-driven. The classes described in the following sections\ndeal with applications, events, and event handling.

# **An Event-driven Graphics Application: I3d_pipeline**

The class `I3d_pipeline`, in file `pipeline.cc`, is an abstract class representing your appli\ncation. As we saw earlier, you subclass from `I3d_pipeline` to create your application, and\nmust fulfill three responsibilities: creating the screen-access objects, declaring world data, and\nresponding to events.

# **Event Generation: I3d_event_source**

Class `I3d_event_source`, in file `ev_src.h`, is an empty class whose sole purpose is to\nindicate that any class derived from this class is capable of serving as an event source for\nan `I3d_dispatcher` object. A class will inherit, possibly multiply inherit, from `I3d_\nevent_source` if it is usable as a source of events. Class `I3d_screen` inherits from\n`I3d_event_source`.