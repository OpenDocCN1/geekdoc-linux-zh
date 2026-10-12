![](bbox=[0.36, 0.14, 0.66, 0.45])

**FIGURE 4-7.** Disk cylinders

Full disk seeks occur when the armature must move from the outermost track to the innermost track or vice versa. Track-to-track seeks involve the armature moving from one track to an adjacent track, hence the name track-to-track seek. Random seeks are somewhere between the other two. This is the type of seek that we are most concerned about, since full disk seeks rarely, if ever, occur.

The full disk seek time of a high performance SCSI disk drive is approximately 7.5 ms for reads and 8 ms for writes. Although full disk seeks rarely occur, the full disk seek time is provided in order to give you a worst-case scenario.

The random seek time for a high performance SCSI disk drive is approximately 3.9 ms for reads and 4.5 ms for writes. This is the type of seek that is very likely to cause performance problems.

The track-to-track seek time for this same SCSI disk drive is 0.5 ms for reads and 0.7 ms for writes. You can see that the track-to-track seek time is considerably less than the random seek times.

**Rotational Latency** Once the armature has completed, the seek to the track where the data resides must then wait for the platter to spin underneath it to where the data resides. The time it takes for the data to move under the head is called the rotational