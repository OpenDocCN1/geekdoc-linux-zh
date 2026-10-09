
## Class `vertex`

Class `vertex` is a `vertex` in 3D space. Member variables `x`, `y`, and `z` are the spatial coordinates. Operator `==` tests for equality of two `vertex` objects by comparing their coordinates, with a slight epsilon parameter to allow for nearby points to be counted as equal.

Listing 6-13: `nl_vertex.h`

```cpp
#ifndef __NL_VERTEX_H
#define __NL_VERTEX_H

struct vertex {
    float x, y, z;

    int operator==(const vertex &r) {
        return(
            -0.001 < x-r.x && x-r.x < 0.001 &&
            -0.001 < y-r.y && y-r.y < 0.001 &&
            -0.001 < z-r.z && z-r.z < 0.001
        );
    }
};

#endif
```

## Class `blender_config`

Class `blender_config` stores the Blender configuration data which `blend_at` must know in order to operate.

- Member `blender_path` is a string storing the directory name where the Blender work file is located.
- Member `blender_work_filename` is a string storing the filename of the Blender work file.
- Member `db_path` is a string storing the directory in which the attribute files will be saved.
- Member `oid_filename` is a string storing the filename in which `blend_at` stores a counter indicating the last ID number it assigned to a mesh. This counter is increased by one every time a mesh gets assigned a new ID, so that meshes always get unique ID numbers.
- Constant `BLENDER_MAGIC_X_SIZE` is a floating-point value that determines the spatial size of the magic edges which get inserted into the geometry to encode the ID. By default, the size is 1.0.
- Constant `ATTRIB_FNAME` is a string containing the prefix of all attribute filenames. By default, the prefix is the string `attrib`, leading to attribute filenames of the form `attribXXX.dat`.

Listing 6-14: `nl_blender_config.h`

```cpp
#ifndef __BLENDER_CONFIG_H
#define __BLENDER_CONFIG_H

#include <string>

class blender_config {
public:
    string blender_path;
    string blender_work_filename;
    string db_path;
    string oid_filename;

    static float BLENDER_MAGIC_X_SIZE;
    static char ATTRIB_FNAME[];
};

#endif
```

Listing 6-15: `nl_blender_config.cc`

```cpp
#include "nl_blender_config.h"

float blender_config::BLENDER_MAGIC_X_SIZE = 1.0;
char blender_config::ATTRIB_FNAME[] = "attrib";
```

## Class `blender_controller`

Class `blender_controller` is an abstract interface for remote control of Blender.

- Member variable `blender_config` points to a Blender configuration object that stores important directory names and filenames.
- Member variable `current_id` is an integer representing the ID of the mesh currently selected in Blender.
- Member variable `current_prop_filename` is the full path to the current attributes file corresponding to the ID stored in `current_id`.
- Member variable `property_lines` is a string list containing the contents of the current attributes file.
- Member variable `selected_faces` is a list of integers indicating the indices of the faces which are currently selected in Blender.

Pure virtual method `find_blender_window` asks the controller to find the current Blender window and to somehow internally store a reference to this window, so that later commands can reference the Blender window. Exactly how the controller finds and stores a reference to the window depends on the windowing system, and is implemented in a subclass.

Pure virtual method `press_key` asks the controller to simulate a key-press event and send it to the Blender window.

Pure virtual method `release_key` asks the controller to simulate a key-release event and send it to the Blender window.

Pure virtual method `read_properties` asks the controller to extract the ID of the currently selected mesh in Blender, then to read the mesh’s properties (the contents of its attributes files) into memory. If the currently selected mesh does not yet have an ID, then `read_properties` should create a new ID, embed the new ID in the mesh, reload the mesh, create an empty attributes file, and read this empty attributes file into memory.

Pure virtual method `determine_selected_face_nums` asks the controller to determine the indices of the faces currently selected in Blender, and to store this list in `selected_faces`. This list, as we saw earlier, is used by the New Face Property button to create new `<X>` properties based on the currently selected faces.

Listing 6-16: `nl_blender_controller.h`

```cpp
#ifndef _NL_BLENDER_CONTROLLER_H
#define _NL_BLENDER_CONTROLLER_H

#include <vector>

class blender_config;

class blender_controller {
public:
    blender_config *config;

    virtual void find_blender_window(void) = 0;
    virtual void press_key(int code) = 0;
    virtual void release_key(int code) = 0;
    virtual void read_properties(void) = 0;
    virtual void determine_selected_face_nums(void) = 0;

    int current_id;
    char current_prop_filename[4096];
    vector<int> selected_faces;
    vector<string> property_lines;
};

#endif
```

## Class `blender_xcontroller`

Class `blender_xcontroller` is a Blender controller for the X Window System.

- Member variable `dpy` stores a pointer to the X Display.
- Member variable `blender_w` stores a reference to the Blender window as a `Window` object.

Method `recursive_find_blender_window` recursively traverses all windows in the display until it finds a window with the title Blender. It then stores this window in the variable `blender_w`.

Overridden method `find_blender_window` calls `recursive_find_blender_window` to do the X search for the Blender window.

Overridden method `press_key` creates an event of type `XEvent`, fills the event structure so that it is a key-press event with the given key code, sends the event to the Blender window with `XSendEvent`, and then flushes the event queue with `XFlush` to ensure that the event is sent.

Overridden method `release_key` creates an event of type `XEvent`, fills the event structure so that it is a key-release event with the given key code, sends the event to the Blender window with `XSendEvent`, and then flushes the event queue with `XFlush` to ensure that the event is sent.

Overridden method `read_properties` is probably the most significant method in the entire `blend_at` program. This method sends keystrokes to Blender to cause it to save the currently selected mesh to the work file. Then, the file is read and scanned for an ID, by looking for overlapping edges as described earlier. If no ID is found, a new ID is created and encoded within the mesh; then, the appropriate keystrokes are sent to Blender to cause it to delete the old mesh and reload the new one with the embedded ID. After finding or newly assigning an ID, the attributes file corresponding to the ID is opened, and its contents are read into the `property_lines` list.

Overridden method `determine_selected_face_nums` is the second most significant method in `blend_at`. It determines which faces are selected by sending Blender keystrokes to separate and save the selection and the original mesh; then, it searches for the selected faces within the original mesh and stores their index numbers in the `selected_faces` list.

Listing 6-17: `nl_blender_xcontroller.h`

```cpp
#ifndef __NL_BLENDER_XCONTROLLER_H
#define __NL_BLENDER_XCONTROLLER_H

#include <X11/X.h>
#include <X11/Intrinsic.h>
#include <unistd.h>
#include <stdio.h>
#include <gtk/gtk.h>
#include <vector>
#include <string>

#include "nl_blender_controller.h"

class blender_config;

class blender_xcontroller : public blender_controller {
protected:
    Display *dpy;
    int recursive_find_blender_window(Window w);

public:
    Window blender_w;

    blender_xcontroller(Display *dpy, blender_config *c);
    virtual ~blender_xcontroller(void);
    void find_blender_window(void);
    void press_key(int code);
    void release_key(int code);
    void read_properties(void);
    void determine_selected_face_nums(void);
};

#endif
```

Listing 6-18: `nl_blender_xcontroller.cc`

```cpp
#include "nl_blender_xcontroller.h"
#include "nl_vertex.h"
#include "nl_blender_config.h"

blender_xcontroller::blender_xcontroller(Display *dpy, blender_config *c) {
    this->dpy = dpy;
    config = c;
    find_blender_window();
}

blender_xcontroller::~blender_xcontroller(void) {
    delete config;
}

int blender_xcontroller::recursive_find_blender_window(Window w) {
    Window root_return, parent_return, *children;
    unsigned int nchildren;
```
