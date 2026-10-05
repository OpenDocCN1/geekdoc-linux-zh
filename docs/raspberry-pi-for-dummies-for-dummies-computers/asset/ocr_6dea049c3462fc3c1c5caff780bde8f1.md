What you should not do is attempt to use these holes by simply pushing wires into them. This is an unreliable way of getting a connection that inevitably leads to damaging your Pi.

Normally, this process would involve soldering, which some people might find off-putting, so the people at Pimoroni have a solution involving a compression eyelet header and a hammer. See https://shop.pimoroni.com/products/gpio-hammer-header.

However, a header is not too difficult to solder up with a fine-tipped iron. Though we cover soldering in general in Chapter 15, here are some extra tips about soldering on a header. Push the header sockets into the holes and turn the board upside down so it rests on the pins. Use a large lump of bulk to make everything level and stable. Place an iron so its tip touches both the pin and the printed circuit board hole, and then apply a little solder. You should see the solder flow keep the iron in place and after a half or so, you'll see the solder sucked into the hole by capillary action of the hammer and molten solder. When you see that, remove the iron. Don't move it until it cools. If the solder isn't pulled in, you will have too much solder, or your soldering isn't hot enough.

Now, before you solder another pin, ensure that the header strip is lying flat on the board. If it isn't, melt the joint again, and push the header strip flat. (Remember: You can't connect a crooked connector after more than one pin has been soldered.) Then proceed and solder it.

If you have trouble with later joints, it's probably because your soldering iron cooled a bit after making a joint. If so, allow a few seconds between joints to warm it up again. Wipe the iron on a damp sponge after each joint, to remove any flux.

Though this seems complex when written down do you, in practice it's much easier and quicker. Figure 16-3 shows a close-up of a header in the process of being soldered.

# Getting at all the pins with one connector

Though a template is useful for identifying individual pins, you might want to transfer the pins to a solderless breadboard, which consists of rows of sockets you can plug wires and other components into. This is a popular way of making a temporary circuit that is quick to change. One way of doing this is with a device called a cobbler, which consists of a ribbon cable and a printed circuit board.