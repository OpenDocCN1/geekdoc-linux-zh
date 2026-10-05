
random elements. That ensures that you remain in control as a composer and know what the music will sound like for your listeners, even with an element of chance in the composition.

If you want to change the sequence to a different one, you can change the *seed*, which is the starting point for generating random numbers. By default it's set to 0. Add the line below at the start of your program for generating random tunes using shuffle, and then run your program:

```
use_random_seed 10
```

Try changing the seed to different numbers, and run the program again to see how the sequence changes.

# Using List Names in Your Programs

The lists of notes and values can make your program look cluttered, but you can tidy your program by giving the lists names and using those names in place of the lists. You can streamline your previous program like this:

```
use_random_seed 10
note_pitches = [:c4, :d4, :e4, :f4, :g4, :a4, :c5]
note_timings = [0.5, 0.5, 1, 0.5, 0.5, 1, 2]
4.times do
    play_pattern_timed note_pitches.shuffle, note_timings
end
play 60
```

# Playing Random Notes

You can play random number numbers, like this:

```
lowest_note = 60
highest_note = 84
6.times do
    play rrand_i(lowest_note, highest_note)
    sleep 0.5
end
```

Try this program in a new buffer. In this program, lowest_note and highest_note are variables. The rrand_i() function gives you a random whole number (or integer). You give the function the lowest and highest possible number you want the computer to pick from. As with the shuffle method, each time you run the program, it generates the same random numbers, so the music sounds the same.
You can change the random seed to get a new melody. (See the section in this chapter on creating random tunes with shuffle.)

The problem with generating random number notes is that not all notes sound good. Before this example, we've been using the notes from the white keys on the piano (the scale of C major) and many of the sharp notes. When you start tuning in sharp notes, the random music can do, starts to sound too chaotic. An alternative way to pick a random note is to create a list of the notes you like (the scale of C major we've been using) and then use the choose() method to pick a random note from it. Here's an

```
note_pitches = [:c4, :d4, :e4, :f4, :g4, :a4, :c5]
loop do
    play note_pitches.choose()
    sleep 0.5
end
```

That program uses a loop that repeats forever, so it'll keep improving until you click the Stop button.

The Log shows you the notes that are played, so you can use this to see which notes are being chosen and confirm that your program is behaving as you expect.

![](img/df9a01bf057d58c2401b5edabd6e8829_304_0.png)

# Experimenting with Live Loops

One of the best features of Sonic Pi is the live loop, which enables you to change your music while it repeats.

The following program modifies the previous example by turning it into a live loop and adding tempo (BPM is short for beats per minute), synth, and option choices. Changing the synth is like changing the instrument the notes are played on. Options (or opts) can be added after the instruction to play a note and affect how the note is played on that instrument. The attack option changes how long a note takes to reach its full volume, for example.

CHAPTER 14 Making Music with Sonic Pi 289

The new lines are bold in the following code:

```
note_pitches = [:c4, :d4, :e4, :f4, :g4, :a4, :c5]
live_loop = :endless_notes do
use_bpm 120
use_synth :doll_bell
play note_pitches.choose(), attack: 0.01
sleep 0.5
end
```

Take care with where you put spaces around colons. In Sonic Pi, colons are used immediately before something (such as a live loop, sample, synth, or chord). The program won't work if you put a space between the colon and the synth name. Colons are also used to separate a parameter (or something you change) from its. In this example, attack is a parameter. The colon must go immediately after the parameter name.

![](img/df9a01bf057d58c2401b5edabd6e8829_305_0.png)

Note that you need a live loop name. This program uses :endless_notes, but you could choose something else if you prefer.

When you run the program, you will hear the new synth sound (:doll_bell), and notice the new tempo.

The clever bit is you can make changes to the program and have them incorporated seamlessly into the music. For example, changing the synth to :chipbass and clicking the Run. The button tunes instruments, but everything remains in time. Try changing the BPM to 60 and clicking the Run to hear the music slow. Change the attack to 1, and you'll hear the sharp percussive sound of the instrument change to a slow drone, almost like a church organ. You can add options to the same play instruction, as long as you separate them with a comma.

![](img/df9a01bf057d58c2401b5edabd6e8829_305_1.png)

To Sonic Pi that you've finished making changes and to hear them in your music, you must click Run again.

The Help pane includes a list of synths you can choose from. Show the Help pane and then click Synths at the bottom. For each synth, there is information about the available options, and useful number values to tri.

For more fluid experimentation, the autocomplete feature can be used while you're writing your code. When you want to change synth, for example, delete the name of the current synth, highlight it before, and then tap after use_synth to see the list of available synths in the autocomplete menu. (See Figure 14-2.) Click one in the menu, or highlight it using the cursor keys and select it by pressing Tab or Enter. This is a great way to enter your code, but also a great way to explore synths and options available.

290 PART 4 Programming the Raspberry Pi

```
note_pitches = [60, 62, 64, 65, 67, 69, 72]
live_loop = endless_notes(note_pitches)
use_synth()
play(live_loop,
    sleep=0.2,
    # slide
    # chitbass
    # chiptune
    # chiptoise
    # voice
    # ambience
    # reverb
    # itdri
    # drill bell
))
```

FIGURE 14-2:
Choosing a
synth using the
autocomplete
feature.

![](img/df9a01bf057d58c2401b5edabd6e8829_306_0.png)

If you press Run multiple times in a program that doesn't use a live loop, you will hear multiple instances of the music at the same time, with no synchronization tween them.

# Using Samples

The programs you've made so far are an interesting way to explore computer music, especially when the computer starts surprising with its random compositions.

Sonic Pi can also use samples, which are snippets of music that you can manipulate, such as by changing their speed or adding effects to them. Sonic Pi includes a wide range of samples, and you can see a list of them by showing the Help pane then using the Sample button in the bottom left. They're especially useful for adding drum loops to your music.

Here's one of our favorites:

```
sample :loop_industrial
```

Put that into a new buffer and click Run to hear it. You can speed up or slow down by changing its rate. Here's how you make it play at half its normal speed:

```
sample :loop_industrial, rate: 0.5
```

We can repeat that sample to make a continuous rhythm. Here did we did when playing notes, we use the sleep command to put a pause between each repetition. Samples can be different lengths, however, which can make it difficult to work out how long to sleep. Luckily, Sonic Pi provides a feature in the language to stretch a sample over a certain number of beats, which solves this problem. can use it like this:

```
do
sample :loop_industrial, beat_stretch: 2
sleep 2
end
```

Now the sample is stretched over 2 beats, and there is a 2-beat pause between each repetition. As a result, you can hear a continuous rhythm. As you saw experimenting with live loops, you can change the tempo with the use_bpm command.

# Adding Special Effects

You can play a sample and add effects to it, including distortion, echo, and reverb. There is a full list of effects (also known as Fx) in the Help pane, and you can also find them using the autocomplete feature. This is how you add to one of the guitar samples:

```
with_fx :distortion do
sample :guit_e_eighths
end
```

You can adjust how the effect is applied to the sound using sounding options. There are several options for distortion, including distort, which controls how much the sound is distorted, and mix, which controls the balance between the original sound and the distorted version. In both cases, the value should be between 0 and 1. Here is how you use them:

```
with_fx :distortion, distort: 0.9, mix: 0.5 do
sample :guit_e_eighths
end
```

Try using different values for those options and running the code to see how the sound changes. Experiment with other effects too.

> To see the full options for any other effect, click Fx in the Help pane, or click the effect name in your code and use Ctrl+I to jump to its entry (available) in the Help. You can also use Ctrl+I to get help on commands in your code.

![](img/df9a01bf057d58c2401b5edabd6e8829_307_0.png)
