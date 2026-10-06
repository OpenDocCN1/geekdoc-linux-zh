# Segment Register Assumptions for Real Mode Segmented Model

Once the segmented modes are so awful is that there is a whole layer of assumptions to be remembered about which segments are used in which ways with which instructions, and what may be overridden with override prefixes. Here’s a quick summary you can refer to if it ever gets all turned around in your head. Keep in mind that this applies only to real mode segmented model. In 32-bit protected mode (as in Linux), all the segments point to the same memory space, and thus you don’t need to “mess with” segments and overrides.

Where allowed, segment assumptions may be overridden with the segment override prefixes. These are DS; SS; CS; and ES. Under NASM, they must be placed inside the memory reference brackets. (MASM and TASM place them outside the brackets.) Here’s an example of such an action in:

```
mov [ES:BX], AX
```

The assumptions are these:

+   1. When the offset is specified in BX, SI, or DI, the assumed segment register is DS.

+   2. When the offset is specified in SP, the assumed segment register is SS. This may not be overridden!