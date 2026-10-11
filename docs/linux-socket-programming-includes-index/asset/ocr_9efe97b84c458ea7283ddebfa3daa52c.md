A programming example might be `SerialPort is a CharDevice, and a CharDevice is a Device.` `Device` would define the basic interfaces for `initialize()`, `open()`, `read()`, `write()`, and `close()`. `CharDevice` would extend `Device`'s interface with `ioctl()`. Lastly, `SerialPort` actually defines the implementation of each interface, applying the serial port's eccentricities.

# ## Data Abstraction

The third foundation, data abstraction, is similar to the abstract programming model described earlier, but it extends the concept a little. Abstract programming allows the programmer to focus on the function and ignores the meaning of the data. This led to standard implementations of basic computer science structures, such as stacks and dictionaries.

Object programming extends this concept with a few of its own. By tacking on encapsulation, object programming allows you to work inside the sphere of the module you need to write and perfect. Abstraction works with the functions and operations from a generic viewpoint.

Abstraction gets a tremendous boost from inheritance. Inheritance coupled with abstraction allows you to create generalized objects that act as blueprints but really don't exist in nature. Taking an example from nature, a Chihuahua is a dog, and a dog is a mammal. Neither dog nor mammal exists in nature, but they do provide a blueprint for how to distinguish the dog from a cat or tree. An abstract object identifies the main responsibilities of the object and may leave some defined but not implemented.

Unlike an abstract object, all normal objects may define and implement all remaining behaviors. In the `Device` example shown previously, `CharDevice` and `Device` are not real objects but merely abstractions that provide blueprints for specific interfaces and behaviors. The behaviors are the basic interfaces mentioned earlier. You may note that you could program the default behaviors for a few interfaces; this would not reduce the power of abstraction. In fact, if done properly, the default behaviors would stand as a basis for the inherited objects would enhance.

Abstraction's power lets you call a single interface (for example, `read()`) from the earlier example) without knowing the specific implementation. The `Device` hierarchy definition (Figure 11.1) includes two other objects, `Disk` and `Network`. Abstraction lets you create any one of the non-abstract objects yet treat them like the abstract version. For example, you can do the following:

```
```c
/*****/
/* Create a Disk object and place it in the Device     */
/* abstract reference                                    */
/*****/
Device *dev = new Disk();
dev->Initialize();
```
```