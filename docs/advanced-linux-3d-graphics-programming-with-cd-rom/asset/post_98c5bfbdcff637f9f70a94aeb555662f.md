
The second responsibility of an `l3d_pipeline` subclass, declaring data, is also intuitive. Since it represents the application, the pipeline subclass must contain all data necessary for maintaining and updating the current state of everything within the virtual world. This might include such things as the current positions and velocities for objects of interest, energy levels for spaceships, the prevailing wind velocity, or anything else being modeled. All of this data is stored within the `l3d_pipeline` subclass in the form of member variables or objects.

The third and final responsibility of an `l3d_pipeline` subclass is to override virtual event functions to respond to events. An `l3d_pipeline` subclass can override any of the following virtual functions declared in `l3d_pipeline`:

```
void key_event(int ch); // from dispatcher
void update_event(void); // from dispatcher
void draw_event(void); // from dispatcher
```

The `key_event` function is automatically called whenever a key is pressed in the application window. The function is called with a parameter indicating the ASCII value of the key pressed, thereby allowing the application to respond to the particular key pressed.

The `update_event` function is automatically called whenever the application is allowed to update itself. You can think of your program as being a giant clockwork, with everything happening at each “tick” of the clock. This event function represents one “tick” in your program. At this point you update the internal variables storing the positions of various objects, update velocities, check for collisions, and so on.

> **TIP**
> The calling frequency of `update_event` is not necessarily guaranteed to be constant. That is to say, the amount of physical time which elapses between successive calls may be slightly different. For accurate physical simulations, where velocities or other physical quantities should be updated based on time, you can store an internal variable recording the value of the system clock the last time that `update_event` was called. We can then compare the current system clock to the value of the variable to determine how much physical time has elapsed, and update the time-dependent quantities accordingly. The particle system program later in this book presents one example of such code.

The `draw_event` function is called whenever the application is allowed to draw its output to the screen. This function typically will be called immediately after `update_event`, but this does not necessarily have to be the case. In other words, the updating of the virtual world and the drawing of the virtual world can be thought of as two separate threads of control, which are usually but not necessarily synchronized.

With this general understanding of a pipeline’s structure (creation of screen, storage of variables, and response to events), we can take a closer look at the particular details of the pipeline in the `drawdot` program.

The constructor for the `drawdot` pipeline takes care of the first responsibility of an `l3d_pipeline` subclass: creation of screen, rasterizer implementation, and rasterizer objects. In the constructor, we first ask the screen factory to create a screen and the rasterizer implementation factory to create a rasterizer implementation. We then create a rasterizer which uses the created rasterizer implementation. The member variables `s`, `rii`, and `r` represent the screen, rasterizer implementation, and rasterizer, respectively.

The constructor also takes care of the second responsibility of an `l3d_pipeline` subclass: management of data representing your virtual world. In our case, our virtual world consists of a single pixel (a humble start). The following member variables are declared and initialized to keep track of the dot's status: `color`, `x, y, dx, and dy`. Variables `x, y, dx, and dy` represent the dot's current horizontal and vertical positions and velocities, and are all initialized to zero. The variable `color` represents the dot's current color, and is specified as follows. First, we logically define the maximum red, green, and blue values to be 255. Then, we specify a color of (0, 255, 128), which means a red intensity of 0, a green intensity of 255, and a blue intensity of 128, all being measured in relation to the logical maximum of 255 which we just set. Finally, we convert this RGB color to a “native” color appropriate for the current screen’s color depth and color model. The conversion is done via an object of type `l3d_screen_info`, which encapsulates the complicated color calculation discussed earlier. The color conversion function is called `ext_to_native`, as it changes a color from an “external” RGB format into a format “native” to the XImage.

The `drawdot` pipeline then overrides the `key_event`, `update_event`, and `draw_event` methods to respond to events. This fulfills the third and final responsibility of an `l3d_pipeline` subclass, responding to events.

The `key_event` for the `drawdot` pipeline checks to see if any one of the directional keys was pressed, and updates the `dx` and `dy` variables, representing the horizontal and vertical velocities, accordingly.

The `update_event` for the `drawdot` pipeline adds the velocities to the positional variables, and makes sure the position stays within the bounds of the screen. In other words, `x += dx` and `y += dy`.

The `draw_event` for the `drawdot` pipeline first calls the `draw_point` routine of the rasterizer, which then forwards the request to the rasterizer implementation to draw a pixel at a particular point in a particular color. Remember that the drawing occurs off-screen (double buffering). The pixel color must be specified in “native” format for the current color depth and color model. We already computed and stored this color earlier by using the function `l3d_screen_info::ext_to_native`. After plotting the point, we call `blit_screen` to cause the off-screen graphics to be copied to the screen.

Let us summarize the main idea behind the pipeline. A pipeline represents the main functionality of an application and is subclassed from `l3d_pipeline`. An `l3d_pipeline` subclass has three responsibilities: creating screen-access objects, declaring world data, and responding to events. Creating screen-access objects (screen, rasterizer implementation, and rasterizer) allows access to the screen and screen-drawing functions. Declaring world data allows the program to keep track of the state of all objects in the virtual world. Responding to events is how the pipeline responds to input (through `key_event`), updates the virtual world (through `update_event`), and draws to the screen (through `draw_event`, using the previously created screen-access objects).

The pipeline does not need to worry about how or when events occur; it merely responds to them. The pipeline’s virtual event functions are thus called from an outside source. This outside source is the *dispatcher*.

## Step 3. Create a Dispatcher

The third step in writing an `l3d` application is to create an *event dispatcher* object. The event dispatcher serves as an interface between an event source and an event receiver. The event receiver in our case is the *pipeline*. The event source is a window created under a *system*-driven windowing *system*. The role of the dispatcher is to receive events from the system-specific window, and to call the appropriate pipeline functions to allow the pipeline to respond to the events.

The whole idea is to isolate the pipeline (i.e., your application logic) from the details of the underlying event-generating mechanism. This way, the pipeline’s logic can focus exclusively on application-specific responses to events, without needing to know exactly how the windowing system generates and transmits events. The dispatcher handles all the messy details of event capturing and translates this into a clean, simple, virtual function call to the pipeline. This allows your pipeline to work on a variety of platforms, with a variety of event-generating mechanisms.

The event dispatcher must be created using the factory chosen in step 1. This is because the dispatcher represents system-specific code, and should thus be created through an abstract factory.

## Step 4. Create a Pipeline

The fourth step in creating an `l3d` application is to create your pipeline object. This step is easy. Having already declared and defined an `l3d_pipeline` subclass, which fulfills the three pipeline responsibilities (creating screen-access objects, declaring world data, and overriding event-handling functions), we simply create the pipeline directly with the `C++` `new` operator. This, in turn, invokes the pipeline’s constructor, which creates the screen, rasterizer implementation, and rasterizer objects.

At this point, the application is ready to respond to events. We just need to pump events to the pipeline in order to allow it to respond to input, update itself internally, and draw to the screen. To start the entire event process, we start the dispatcher.

## Step 5. Start the Dispatcher

The fifth step in writing an `l3d` application is to start the dispatcher. We must do three things:

- Assign a pipeline to the dispatcher.
- Assign an event source to the dispatcher.
- Call `start`.

A moment’s reflection makes it clear why the two assignments are necessary. The dispatcher takes events from the event source, interprets them minimally, and calls the appropriate pipeline virtual event function to allow the pipeline to respond. The `pipeline` member of the dispatcher object is set to the pipeline we just created. The `event_source` member of the dispatcher object is set to the screen object created in the pipeline’s constructor—in other words, the screen (in our case, the X window) is the source of events. With these two member variables set, the dispatcher can then begin to extract events from `event_source` and pass them on to `pipeline`—a process set in motion by calling `start`.
