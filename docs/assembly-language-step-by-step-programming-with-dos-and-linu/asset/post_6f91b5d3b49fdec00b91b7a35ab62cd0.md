
should instead think of strings in much the same way you think of segments: in terms of the register values that define them.

It's slightly inside-out compared to how you think of strings in such languages: You've got a string when you set up a pair of registers to point to one (or a single register, if you're working in real mode or protected mode flat model). And once you point to a string, the length of string is defined by the value you place in register CX.

This is key: Assembly strings are wholly defined by values you place in registers. There is a set of assumptions about strings and registers baked into the silicon of the CPU. When you execute one of the string instructions (as I describe a little later), the CPU uses those assumptions to determine which area of memory it reads or writes to.

## Source Strings and Destination Strings

There are two kinds of strings in assembly work. Source strings are strings that you read from. Destination strings are strings that you write to. The difference between the two is only a matter of registers; source and destination strings can overlap. In fact, the very same region of memory can be both a source string and a destination string, all at the same time.

Here are the assumptions the CPU makes about strings when it executes a string instruction:

- A source string is pointed to by DS:SI.
- A destination string is pointed to by ES:DI.
- The length of both kinds of strings is the value you place in CX.
- Data coming from a source string or going to a destination string must pass through register AX.

Note that the use of segment registers mostly applies to real mode segmented model. In real mode flat model, as you should know by now, all the segment registers contain the same value, and are therefore basically factored out of consideration for many things, string work included. (The same is true of protected mode flat model, as you'll learn in later chapters.) The CPU can recognize both a source string and a destination string simultaneously, because DS:SI and ES:DI can hold values independent of one another. However, because there is only one CX register, the length of source and destination strings must be identical when they are used simultaneously, as in copying a source string to a destination string.

## ASSEMBLY LANGUAGE STEP-BY-STEP

One way to remember the difference between source strings and destination strings is by their offset registers. SI means “source index,” and DI means “destination index.”

## REP STOSW, the Software Machine Gun

The best way to cement all that string background information in your mind is to see a string instruction at work. In this section I lay out a useful video display tool that makes use of the simplest string instruction, STOSW. (Think: STore String by Word.) The discussion involves something called a prefix, which I haven’t gone into yet. Bear with me for now. We’ll discuss prefixes in a little while.

## Machine-Gunning the Video Display Buffer

The Clr procedure we discussed earlier relied on BIOS to handle the actual clearing of the screen. BIOS is very much a black box, and we’re not expected to know how it works. The trouble with BIOS is that it only knows how to clear the screen to blanks. Some programs (such as the most recent releases of Borland/Turbo Pascal) give themselves a stylish, sculpted look by clearing the screen to the PC’s halftone characters, which are character codes 176 to 178. BIOS can’t do this. If you want the halftone look, you’ll have to do it yourself. It doesn’t involve anything more complex than replicating a single string word (two bytes) into every position in your video refresh buffer.

Such things should always be done in tight loops. The obvious way is to put the video refresh buffer into extra register ES, the refresh buffer offset into DI, the number of words in your refresh buffer into CX, the video value to clear the buffer into AX, and then a code tight this way:

```
Clear: mov ES,[DI],AX ; Copy AX to ES:DI
      inc DI            ; Dump DI to next *word* in buffer,
      inc DI            ; means incrementing by 1 twice
      dec CX            ; Decrement CX by one position
      jnz Clear         ; Loop again until CX is 0
```

This will work. It’s even tolerably fast, especially on newer CPUs. All of the preceding code is equivalent to this one instruction:

```
rep stosw
```

Really. Really.

There are two parts to this instruction, actually. As I said, REP is a new type of critter, called a prefix. We'll get back to it. Right now, let's look at STOSW. The mnemonic STOREs String by Word. Like all the string instructions, STOSW makes certain assumptions about some CPU registers. It works only on the destination string, so DS and SI are not involved. However, these assumptions must be respected and dealt with:

1. ES must be loaded with the segment address of the destination string (that is, the string into which data will be stored). This is automatically the case in flat model and does not have to be set up by you.
2. DI must be loaded with the offset address of the destination string. (Think: DI, the destination index).
3. CX (think: the Count register) must be loaded with the number of times the copy of AX is to stored into the string. Note that this does not mean the size of the string in bytes!
4. AX must be loaded with the word value to be stored into the string.

## Executing the STOSW Instruction

Once you set up these four registers, you can safely execute a STOSW instruction. When you do, this is what happens:

- 1. ES must be loaded with the segment address of the destination string (that is, the string into which data will be stored). This is automatically the case in flat model and does not have to be set up by you.
- 2. DI must be loaded with the offset address of the destination string. (Think: DI, the destination index).
- 3. CX (think: the Count register) must be loaded with the number of times the copy of AX is to stored into the string. Note that this does not mean the size of the string in bytes!
- 4. AX must be loaded with the word value to be stored into the string.

Wait, the OCR text for the last section has some repetitions/interleaving. Let me re-align the logical flow properly:

Once you set up these four registers, you can safely execute a STOSW instruction. When you do, this is what happens:

- 1. The value in AX is copied to ES:DI.
- 2. DI is incremented by 2 to point to the next word.
- 3. CX is decremented by 1.
- 4. This repeats until CX is 0.

However, this is the difference between a semiaomatic weapon (which fires every time you pull and release the trigger) and a fully automatic weapon, which fires continuously as long as you hold the trigger down. To make STOSW fully automatic, just hang the REP prefix ahead of it. What REP does is beautifully simple: It sets up the tightest of all loops inside the CPU and fires copies of AX into memory repeatedly, incrementing DI by 2 each time and decrementing CX by 1 until CX is zero. It stops, and when the smoke clears, you'll see that your whole destination string, however large, has been filled with copies of AX.

Man, now that's programming!

The following macro sets and triggers REP STOSW to clear the refresh buffer. Clear was designed to be used with the block of video information initialized by the Vid procedure. It needs to be passed a far pointer (which is nothing more than a full 32-bit address consisting of a segment and an offset) to the video refresh buffer, and the word value to be blasted into the buffer.

```
; CLEAR -- Clears the entire visible screen buffer
; Last update 9/20/99
; Caller pass: The address of the video refresh buffer
; InClearAtom: The character/attribute pair to fill the
buffer with. The high byte contains the
attribute and the low byte the character.
; InBufLength: The number of 'characters' in the visible
display buffer, 'not' the number of bytes!
This is typically 2000 for a 25-line screen
or 4000 for a 50-line screen.
```

```
@macro Clear 3 :VidAddress,ClearAtom,BufLength
les DI,[1] ; Load ES and DI from FAR pointer
mov AX,%2 ; Load AX with word to blast into memory
mov CX,%3 ; Load CX with length of bytes by 2 for word
shr CX,1 ; Divide size of buffer by word count
cld ; Set direction flag so we blast up-memory
```
