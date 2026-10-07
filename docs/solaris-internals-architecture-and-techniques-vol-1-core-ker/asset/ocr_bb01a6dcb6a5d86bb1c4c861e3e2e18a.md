mine if the lock is held or not, another thread executing on another processor
issues a lock call to get the same lock at the same time. If the lock is not held, both
threads would assume the lock is available and would issue a store to hold the
lock. Obviously, more than one thread cannot own the same lock at the same time,
but that would be the result of a sequence of events. Atomic instructions pre-
vent things from happening.

SPARC processors implement memory access instructions that provide atomic
test-and-set instructions for mutual exclusion, as well as instructions that
can force a particular ordering of memory operations (more on the latter feature in
a moment). UltraSPARC processors (the SPARC V9 instruction set) provide three
memory access instructions that guarantee atomic behavior: ldstub (load and
store unsigned byte), cas (compare and swap), and swap (swap byte locations).
These instructions differ slightly in their behavior and the size of the datum they
operate on.

Figure 3.2 illustrates the ldstub and cas instructions. The swap instruction
(not shown) simply swaps a 32-bit value between a hardware register and a mem-
yory, similar to what cas does if the compare phase of the instruction
sequence is equal.

The implementation of locking code with the assembly language test-and-set
style of instructions requires a subsequent test instruction on the lock value, which
is retrieved with either a cas or ldstub instruction.

For example, the ldstub instruction retrieves the byte value (the lock) from
nory and stores it in the specified hardware register. Locking code must test
the value of the register to determine if the lock was held or available when the
lstub executed. If the register value is all 1s, the lock was held, so the code must
branch off and deal with that condition. If the register value is all 0s, the lock was
not held and the code can progress as being the current lock holder. Note that in
both cases, the lock value in memory is set to all 1s, by virtue of the behavior of
lstub instruction (store 0FF at designated address). If the lock was already
held, the value simply didn't change. If the lock was 0 (available), it will now
reflect that the lock is held (all 1s). The code that releases a lock sets the
value to all 0s, indicating the lock is no longer held.