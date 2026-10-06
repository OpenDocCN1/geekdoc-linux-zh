# ASSEMBLY LANGUAGE STEP-BY-STEP

copied into memory. (You may want to do that—there's no law saying you have to fill a string with only one single value.)

However, this is like the difference between a semiaomatic weapon (which fires rounds every time you pull and release the trigger) and a fully automatic weapon, which fires rounds continually as long as you hold the trigger down. To make STOSW fully automatic, just hang the REP prefix ahead of it. What REP does is beautifully simple: It sets up the tightest of all tight loops completely inside the CPU and fires copies of AX into memory repeatedly (hence its name), incrementing DI by 2 each time and decrementing CX by 1, until CX is decremented to 0. It stops, and when the smoke clears, you'll see that your whole destination string, however large, has been filled with copies of AX.

Man, now that's programming!

The following macro sets and triggers REP STOSW to clear the refresh buffer. Clear was designed to be used with the block of video information variables initialized by the VidCheck procedure described in Chapter 10. It needs to be passed a far pointer (which is nothing more than a full 32-bit address consisting of a segment and an offset lead in to end) to the video refresh buffer, and the word value to be blasted into the buffer.

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
or 4000 for a 50-line screen
; Action: Clears the screen by machine-gunning the
character/attribute pair in AX into the
display buffer beginning at Vid.
```

```
@macro Clear 3 :VidAddress,ClearAtom,BufLength
les DI,[1] ; Load ES and DI from FAR pointer
mov AX,%2 ; Load AX with word to blast into memory
mov CX,%3 ; Load CX with length of bytes by 2 for word
shr CX,1 ; Divide size of buffer by word count
cld ; Set direction flag so we blast up-memory
```