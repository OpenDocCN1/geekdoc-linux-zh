
## Synchronizing with Your Drumbeat

You now know how to play a repeating rhythm, and how to play other samples and synth melodies. You can play multiple live loops at the same time. One of the challenges is to synchronize all the parts of the music so they play live. To do that, you can provide an option to synchronize the start of a live loop with the name of another live_loop. Here's an example that synchronizes a cymbal beat with the main drum loop:

```
live_loop :drums do
  sample :loop_industrial, beat_stretch: 2
  sleep 2
end

live_loop :ymbals, sync: :drums do
  4.times do
    sample :elec_cymbal
    sleep 1
  end
  sleep 8
end
```

When you play that example, you'll hear the cymbal plays four times, perfectly sync with the main drum. It rests for 8 beats before playing again.

Take care with the colons when setting the sync option for your live loop; otherwise, the program won't work. The first colon (after sync) goes between the option and its parameter and touches the option name, and the second colon (before drums) marks the start of the loop name you want to synchronize with.

## Bringing It All Together

Listing 4-1 brings together the ideas in this chapter. It uses the loop_Industrial sample as the backbone, with the other live loops synchronized to start in time with it. It is a melody live loop, which plays random notes from the list provided. The list includes some note vocals, as the songs tend towards using the C note more often. There is a loop that plays higher notes quickly over the top, and a bass part that is played using the play_pattern_timed instruction you saw earlier in this chapter. Finally, there is another live loop that adds the amen drumbeat on top, in bursts. It plays 8 times, but the sleep command is used to stop the beat from starting immediately, and to put a gap between each burst.

### LISTING 14-1: Bringing it all together

# Robot jam by Sean McManus
# Music example from Raspberry Pi For Dummies, 3rd Edition

```
live_loop :drums do
  with_fx :krush do
    sample :loop_industrial, beat_stretch: 2
  end
  sleep 2
end
```

```
live_loop :melody, sync: :drums do
  note_pitches = [:c3, :c3, :c3, :d3, :g3, :g3, :a3, :c4, :c4]
  use_synth :saw
  with_fx :wobble do
    play note_pitches.choose()
    sleep 2
  end
end
```

```
live_loop :plinks, sync: :drums do
  plink_pitches = [:c4, :d4, :e4, :g4, :a4]
  use_synth :chiplead
  play plink_pitches.choose()
  sleep 0.25
end
```

```
live_loop :bass, sync: :drums do
  use_synth :tb303
  play_pattern_timed [:c2, :c2, :c2, :c2, :c2, :c2, :g2, :a2], -> [0.5, 0.5, 0.5, 0.5, 0.5, 0.5, 0.5, 0.5]
end
```

```
live_loop :amen, sync: :drums do
  sleep 1.6
  sample :loop_amen, beat_stretch: 2
  sleep 2
end
```

You can use this piece as the basis for your own experiments. Because the sections use live loops, you can modify the effects, options, synths, and notes and then click the Run button to hear your changes.

## Next Steps with Sonic Pi

We hope that this chapter has inspired you to experiment with making music on the Raspberry Pi. You've learned how to play melodies using different synths. You've also discovered several different ways to create improvised music, using random note numbers, and random notes picked from a list. We've shown you how to bring it all together, too, combining and synchronizing samples and synth melodies. Using the code in this chapter, and the rich range of samples and tools that Sonic Pi provides, you can compose your own music.

There's much more you can do with Sonic Pi, including using it with Minecraft and using MIDI signals to connect to other electronic instruments and music software. The Help pane includes a tutorial and a series of articles that were previously published in The MagPi magazine, so there's plenty of support when you're ready to take Sonic Pi further.

Whether you like dance, prog, pop, or rock, Sonic Pi deserves to be in your band.

## 5. Exploring Electronics with the Raspberry Pi

## IN THIS PART ...

- Discover the fundamentals of electricity, how to calculate current, and how to solder.
- Find out how the Raspberry Pi can reach out through its GPIO pins.
- Learn how to control LEDs and read push buttons.
- Create an electronic dice and make a pedestrian crossing simulator.
- Explore the thousands of colors you can make from LEDs.
- Make a Rainbow Invaders game.
- Use RFID (Radio Frequency [Identification]) cards to make a jukebox and dress up a doll.

## Discover What a Circuit

The first thing you have to understand is that a circuit is something where electricity can flow; it is a continuous loop with no dead ends. If you have a dead end, you don't have a circuit. Electricity has to be able to flow. So let's be more specific in what we mean by electricity.

There are two aspects of electricity: current and voltage:

- Current is what actually flows.
- Voltage is what forces the current round a circuit.

Voltage can't flow and current doesn't exist in the absence of voltage. However, voltage can exist in the absence of current.

## Understanding the nature of electricity

So, what is electric current? It is a flow of electrons past a point, just like a flow of cars past a motorway sign. With electric circuits, you measure current in amps. One amp of current is about $6.24 \times 10^{18}$ electrons per passing a point. That's a big number, and fortunately, we don't have to count all those zeroes. The bigger the voltage, the more current is forced through a circuit, but circuits have a property that resists the flow of current. We call this the resistance of a circuit. This resistance depends on the materials the circuit is made from and is measured in a unit called ohms. So, because we know how to define an amp in terms of electron flow, we can define these two properties in terms of an:

One volt is the voltage you need to drive one amp through a circuit with the resistance of one ohm.
