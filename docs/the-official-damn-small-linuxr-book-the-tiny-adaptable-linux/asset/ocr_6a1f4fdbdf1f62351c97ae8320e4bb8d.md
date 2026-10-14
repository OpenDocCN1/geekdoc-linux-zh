Remove the utilities diskette from the drive and insert the first chunk diskette in the floppy drive. Press the Enter key when ready.

Wait for the copy to complete. You see a progress message as the copy is progressing. When the diskette is quiescent, remove the chunk diskette and insert the next one into the drive.

You can use the up arrow key to repeat the copy command `copy b:\chunk*`, then press the Enter key to proceed with the copy.

Repeat this process for all diskettes, which should be between 34 and 35 floppies.

# NOTE

While the copy process is running, you might see a message that says: “Error reading from drive B:...” If that happens, press `a` for abort. Write down this chunk number.

Return to the source machine and do the following:

+   1. Format this “bad read” diskette.
+   2. Mount the newly formatted diskette.
+   3. Try to copy the chunk (`cp chunkxy /mnt/auto/floppy`).
+   4. Type `sync` to sync anything data cache to permanent storage.
+   5. Unmount the floppy disk (`umount /mnt/auto/floppy`).

Back on the target machine, reinsert this floppy, press the Up arrow to recall the copy command, and press Enter. If this diskette still fails, repeat with another new floppy.

After copying all “chunk” diskettes, return to the A: drive prompt. Replace the utilities diskette. This should stop the prompt for any B: drive. Next, move to the `C:\knoppix` folder:

```
A:\> C:
C:\> cd knoppix
C:\KNOPPIX> cat chunk* > knoppix
C:\KNOPPIX> del chunk*
C:\KNOPPIX> a:
A:\>
```