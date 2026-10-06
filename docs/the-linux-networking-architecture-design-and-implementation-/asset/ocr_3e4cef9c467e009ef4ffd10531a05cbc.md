# 434 Chapter 22 Extending the Linux Network Architecture Functionality—KIDS

parameters. The flag parameter shows whether this is the first initialization of this instance (INIT_BHVR) or it is a change to its parameters at runtime, only the information provided should be altered.

destructor(bhvr) is invoked to destroy the bhvr instance of the component. All cleanup work required (e.g. free memory or deactivate timer) should be done at this point.

get_bhvr(bhvr, port) is invoked by KIDS to obtain a pointer to the bhvr structure of the component instance appended to the output, port. The number and names of a component's outputs are individual, so we have to implement a component-specific function.

append_bhvr(new_bhvr, old_bhvr, port) connects the new_bhvr component instance to the output, port, of the existing component instance. old_bhvr. Again, we have to implement separate functions for the individual outputs of a component.

proc(bhvr, ptr, layer) creates information about the bhvr component instance. This information can be output from proc files. The layer parameter specifies the distance from the component instance to the hook; this is required for indenting within the output. The ptr pointer specifies the buffer space this should be written to. (See Section 2.8).

get_config(bhvr, ptr) is invoked by KIDS to write the configuration of the bhvr component instance to the ptr buffer, based on the KIDS configuration syntax (see Section 22.3.6).

```
struct bhvr kids/kids_bhvr.h
```

Each of the bhvr structures representing the specific instances of a component manages the information of a component instance (e.g. on number of references). The bhvr data structure is built as follows:

```
struct bhvr {
    char name[STRLEN];
    unsigned int use_counter;
    struct bhvr *next_bhvr;
    struct bhvr_type *bhvr_type;
    char bhvr_data[0];
}
```

The fields have the following meaning:

name:The name of this instance (e.g. tb0 or marker1);use_counter specifies the number of direct predecessors of this component instance--the number of references to this bhvr.

next_bhvr is used to link the individual bhvr data structures in the bhvr_list. This list is managed by KIDS and used to search for a component by its name (get_bhvr_by_name()).