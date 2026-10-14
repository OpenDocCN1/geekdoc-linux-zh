```
129
130     * to be killed or stopped.
131     */
132     for (i = 0; i < _NSIG_WORDS && !is_sig; i++)
133         is_sig = current->pending.signal.sig[i] &
134             ~current->blocked.sig[i];
135
136     if (is_sig) {
137         /* It is important to put module_put(THIS_MODULE) here, because
138          * for processes where the open is interrupted there will never
139          * be a corresponding close. If we do not decrement the usage
140          * count here, we will be left with a positive usage count
141          * which we will have no way to bring down to zero, giving us
142          * an immortal module, which can only be killed by rebooting
143          * the machine.
144          */
145         module_put(THIS_MODULE);
146         return -EINTR;
147     }
148     }
149
150     return 0; /* Allow the access */
151     }
152
153     /* Called when the /proc file is closed */
154     static int module_close(struct inode *inode, struct file *file)
155     {
156         /* Set already_open to zero, so one of the processes in the waitq will
157          * be able to set already_open back to one and to open the file. All
158          * the other processes will be called when already_open is back to one,
159          * so they'll go back to sleep.
160          */
161         atomic_set(&already_open, 0);
162
163         /* Wake up all the processes in waitq, so if anybody is waiting for the
164          * file, they can have it.
165          */
166         wake_up(&waitq);
167
168         module_put(THIS_MODULE);
169
170         return 0; /* success */
171     }
172
173     /* Structures to register as the /proc file, with pointers to all the relevant
174      * functions.
175      */
176
177     /* File operations for our proc file. This is where we place pointers to all
178      * the functions called when somebody tries to do something to our file. NULL
179      * means we don't want to deal with something.
180      */
181     #ifdef HAVE_PROC_DPS
182     static const struct proc_ops file_ops_4our_proc_file = {
183         .proc_read = module_output, /* "read" from the file */
184         .proc_write = module_input, /* "write" to the file */
185         .proc_open = module_open, /* called when the /proc file is opened */
186         .proc_release = module_close, /* called when it's closed */
```