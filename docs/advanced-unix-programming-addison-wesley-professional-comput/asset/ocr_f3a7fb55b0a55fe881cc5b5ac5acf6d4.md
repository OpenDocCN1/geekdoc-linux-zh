```
```c
default: /* "impossible" case */
errno = 0;
EC_FAIL
}

EC_CLEANUP_BGN
return false;
EC_CLEANUP_END
}
```
```

Both functions return true on success and false on error. The statusp argument gives the result for ready: CR_READY, CR_NOTREADY, or CR_EOF. For cget, the only possibilities are CR_READY and CR_EOF.

We’ve preempted the NUL byte as our empty-buffer indicator (EMPTY), which means that NUL bytes read by cready will be ignored. If this isn’t acceptable, a separate bool variable can be used as an empty-buffer flag.

Notice the way cready and cget shift back and forth between blocking and non-blocking input. Since we’re reading only one input stream, there’s no need to stay in the nonblocking state while we test for an available character, as we had to do in the first, inefficient, version of ready in Section 4.2.2. We revert to blocking and issue a read. After all, waiting for a character is what blocking means.

cready and cget are most useful when a program has some discretionary work to do, work that can be postponed if a character is ready. A good example is a program that uses Curses (Section 4.8). The way Curses works, all the screen output is held in a buffer until refresh is called to send it to the physical screen. This is time-consuming because refresh compares what is currently on the screen with the new image so as to minimize the number of characters transmitted. A fast typist can easily get ahead of the updates, especially if the screen must be updated on each keystroke, as it must with a screen editor. A neat solution is to call refresh from within the input routine, but only if input is not waiting. If input is waiting, then the user has obviously typed ahead without waiting for the screen to catch up, so the screen update is skipped. The screen will be updated the next time the input routine is executed, unless a character is waiting then too. When the user stops typing, the screen will become current. On the other hand, if the program can process characters faster than the typist types them, the screen will get updated with each keystroke.

This may sound complex, but by using functions we’ve already developed, it takes only a few lines of code: