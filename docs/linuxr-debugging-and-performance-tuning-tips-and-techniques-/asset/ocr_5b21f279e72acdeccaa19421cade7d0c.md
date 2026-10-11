```
67      } else if (ret == -1 && errno == EINTR) {
68          write(1, "\nretrying\n", 10);
69          goto retry;
70      } else {
71          strcpy(buf, "twaitpid() failed: ");
72          strcat(buf, strerror(errno));
73          strcat(buf, "\n");
74          write(1, buf, strlen(buf));
75      }
76
77      write(1, exited, strlen(exited));
78  }
```

The signal handler is similar to those shown earlier. Note the argument list (line 39), and that there is no loop.

Lines 49–54 handle process termination, including calling manage() to print the status.

Lines 55–60 handle the case of an unexpected child dying. This case shouldn’t happen, since this signal handler is passed information specific to a particular child process.

Lines 61–66 are what interest us: The return value is 0 for status changes. manage() deals with the details (line 66).

Lines 67–69 handle interrupts, and lines 70–75 deal with errors.

```
80  /* child --- what to do in the child */
81
82  void child(void)
83  {
84      raise(SIGCONT);     /* should be ignored */
85      raise(SIGSTOP);     /* go to sleep, parent wakes us back up */
86      printf("\t--- child restarted ---\n");
87      exit(42);          /* normal exit, let parent get value */
88  }
```

The child() function handles the child’s behavior, taking actions of the sort to cause the parent to be notified.7 Line 84 sends SIGCONT, which might cause the parent to get a CLD_CONTINUED event. Line 85 sends a SIGSTOP, which stops the process (the signal is uncatchable) and causes a CLD_STOPPED event for the parent. Once the parent restarts the child, the child prints a message to show it’s active again and then exits with a distinguished exit status.