# Make music with Sonic Pi

# Projects

# Starting with Sonic Pi

**02** Sonic Pi is located in the Education category in the menus. Open it up and you'll be presented with something that looks like an IDE. The pane on the left allows you to enter the code for your project, with proper syntax highlighting for its own style of language. When running, an info pane details exactly what's being played via Sonic Pi -- and any errors are listed in their own pane as well, for reference.

# Set the beat

**04** For any piece of music, you'll want to set the tempo. We can start by putting `1.itb_tempo 200` at the start of our code. We can test it out by creating a string of midi notes using `play_pattern`:
`play_pattern`
`[40,25,45,25,50,50]`

This will play, pretty, bell notes at those tones at the tempo we've set. You can create longer and shorter strings, and also change the way they play.

# Your first note

**03** Our first thing to try on Sonic Pi is simply being able to play a note. Sonic Pi has a few defaults preset, so we can get started with:
`play 50`
Press the Play button and the output window will show you what's being played. The pretty, bell sound is the default tone for Sonic Pi's output, and 50 determines the pitch and tone of the sound.

![](bbox=[0.36, 0.34, 0.64, 0.43])

![](bbox=[0.75, 0.39, 0.98, 0.49])

# Advance your melody

**05** We can start making more complex melodies by using more of Sonic Pi's functions. You can change the note type by using `with_synth`, reverse a pattern, and even create a finite loop with the x.times function, to end and signify the start and end of the loop. Everything is played in sequence before repeating, much like an if or while loop in normal code.

# Full code listing

```
`with_tempo   200
play_pattern  [40,25,45,25,50,50]
2.times do
  with_synth "beep"
    play_pattern  [40,25,45,25,50,50]
    play_pattern  [40,25,45,25,50,50].reverse
  end
play_pad "saws", 3
in_thread do
  with_synth "fm"
    6.times do
      if rand < 0.5
        play 30
      else
        play 50
      end
      sleep 2
    end
  end
2.times do
  play_synth "pretty_bell"
    play_pattern  [40,25,45,25,50,50]
    play_pattern  [40,25,45,25,50,50].reverse
  end`
```

# Playing a concert

**06** Using the `in_thread` function, we are able to create another thread for the Sonic Pi instance, and have several lines of musical code play at once instead of in sequence.
We have made it create a series of notes in a random sequence, and have them play alongside extra notes created by the position and velocity of the mouse using the `play_pad` function.