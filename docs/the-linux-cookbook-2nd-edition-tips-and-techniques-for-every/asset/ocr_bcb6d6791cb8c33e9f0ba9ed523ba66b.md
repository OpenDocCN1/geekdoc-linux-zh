Selecting a section of a sound file in Snd is similar to selecting text in Emacs; you can mark a section of a sound file or recording you’ve made in Snd by left-clicking and dragging across the area with the mouse. The area you drag across becomes shaded and is called the selection. Once you select a portion of the sound, any effect you choose works on that selection. You can also cut and paste selections of the sound you are editing into other sound buffers.

The xwave tool (and many others, no doubt) have similar capabilities and functions (see Recipe 23.4 [Using Other Sound Editors], page 496).

# 23.1.1 Cutting Out Part of a Sound File

To cut out a portion of a sound file you are editing in Snd, first select that portion by left-clicking and dragging, and then choose Cut from the Edit menu, somewhat like cropping an image file.

# 23.1.2 Pasting a Selection into a Sound File

Paste a cut sound selection into a different sound buffer in Snd by opening the new buffer, left-clicking in the target buffer, and then choosing Paste from the Edit menu. Your most recent selection will be pasted at the point where you clicked in the sound buffer.

# 23.1.3 Mixing Sound Files Together

To mix different audio files together as multiple tracks in Snd, choose Mix from the File menu and specify the files to use as the individual tracks.

# 23.2 Applying Sound Effects

SOund eXchange
DEB: sox
RPM: sox
WWW: http://sox.sourceforge.net/

The “Sound eXchange” tool, sox, is a sound sample translator. It reads sound as files or standard input, and outputs the sound either to a file or standard output, while translating in between. You can use sox to convert sound files from one format to another or to process sounds with special effects. This section describes some of the special effects you can apply to sound files with sox.