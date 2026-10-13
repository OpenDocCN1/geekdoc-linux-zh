kernel maintains the address of the first CPU structure in the linked list in a kernel variable called `cpu_list`.

```
```text
# adb -k
physmem 3b5f
cpu_list/k
cpu_list:
cpu_list:        1041ad20
1041ad20$<cpu

cpu0:
cpu0:            id                 seqid                 flags
                 0                  0                     1b
cpu0+0x10:       thread             idle_thread            pause_thread
                 30000ab8fe0        2a10001fd40            2a1000fd40
                 lwp                parent                 part
cpu0+0x28:       1000007000         0                      1041b e88
                 next               prev                   next_only
cpu0+0x48:       300003d2010        300003d2010            300003d2010
cpu0+0x60:       prev_onln          next_pan               prev_part
                 300003d2010        300003d2010            300003d2010
                 disp
cpu0+0x78:       lock               npri                   queue
                 0                   170                    3000048a000
cpu0+0x88:       limit              actmap                 maxnpri
                 3000048aff0        300004a840             -1
cpu0+0x9a:       max_unb_pri        n runnable
                 -1                  0

cpu0+0xa8:       rqhru n            kprunru                chosen_level
                 0                   0                      -1
cpu0+0xb0:       dispt hread        thread_lock             last_switch
                 30000ab8fe0        0                      12e9f54
cpu0+0xc8:       intr_stack         on_intr                 intr_thread
                 2a10001bf50        0                      300007dd40
cpu0+0xe0:       intr_actv          base_spl                profile_cyclic_id
                 0                  0                      0
cpu0+0x278:      0 profile_pc       profile_pil             profile_when
                 syscall_trap+0x28  0                      0
                 profile_late       cyc_cpu
                 53                  30000067c8
```
```

To look at structures for the remaining processors, feed the next value into the adb cpu macro.

Note the flags field, which is the cpu_flags member. This example represents the state after bootstrap of a CPU that has not had its state altered explicitly. Following initialization, the set cpu_flags bits are CPU_RUNNING,