DEBUG will respond by displaying the current value of AX (here
"0000") and then, on the following line, a colon prompt. It will wait for
you to enter a new numeric value for AX, or for you to press Enter
Enter. If you press Enter, the current value of the register will not be
changed. In the preceding example, I typed "0A7B" (you don't need type)
the H indicating hex) followed by Enter.

Once you do enter a new value and then press Enter, DEBUG does
nothing to verify that the change has been made. To see to reg-\ister AX, you must display all the registers again using the R command:

+   - R
AX=0A7BX=0000 CX=0000 DX=0100 SP=FFEE BP=0000 SI=0100 DI=0000
DS=1980 SS=1980 CS=1980 IP=0100 NV UP EI PL ZE NA NA PC OC
1980:0100 39A5409 CMP [SI+0954], BL SS:0954-8A

Take a few minutes to practice entering new values for the general-purpose registers, then display the registers as a group to verify that the
changes were made. While exploring, you might find that the IP regist-
ter can be changed, even though I said earlier that it can't be changed
directly. The key word is directly, DEBUG knows all the dirty tricks.

# **Inspecting the Video Refresh Buffer with DEBUG**

One good way to help your knowledge of memory addressing sink in is
to use DEBUG to take a look at some interesting places in the PC’s
memory space.

One easy thing to do is look at the PC’s video display adapter’s text
screen refresh buffer. A video refresh buffer is a region of memory
with a difference: Any characters written to buffer memory are instantly
displayed on the computer’s screen. This is accomplished electrically
through special use of the information that comes out of the memory
data pins. Precisely how it is done outside the scope of this book. For
now, simply understand that writing a character to your text mode display screen (which is not the Windows graphical UI screen!) can be
done by writing the ASCII code for that character into the code
address in the video buffer portion of memory.

The text mode display buffer is the screen that appears when you’re
running DOS or else working in a DOS window (or "DOS box") from
within MS Windows. It consists not of icons or graphical images or fig-