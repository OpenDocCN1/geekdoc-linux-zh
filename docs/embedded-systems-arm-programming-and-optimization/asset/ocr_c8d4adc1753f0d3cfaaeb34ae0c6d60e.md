# 294 APPENDIX C OpenCL Reference

| all(x) | Tests if all MSB of all elements is 1 |
| bitselect(a,b,c) | Each bit of result is corresponding bit of a if corresponding bit of c is 0. Otherwise it is the corresponding bit of b. |
| select(a,b,c) | For each component of a vector type, result[i]=if MSB of c is set ? b[i] : a[i]. For scalar type, result=c? b : a |

# C10.6 Atomic functions

Atomic operations allow shared memory locations to be read, modified, and updated in a way that is not interruptible, allowing work-items to perform primitive shared memory operations without a certain critical section.

Note that OpenCL 1.1 and 1.2 do not include any locking functions for kernels, but one can be built using the atomic exchange function.

| atomic_add(*p,val) | Read, add, store Integers only |
| atomic_sub(*p,val) | Read, subtract, and store Integers only |
| atomic_xchg(*p,val) | Read, swap, and store Returns the value swapped out from *p |
| atomic_inc(*p) | Read, increment, and store Integers only |
| atomic_dec(*p) | Read, decrement, and store Integers only |
| atomic_cmpxchg(*p,cmp,val) | Read, store only if memory contents match |
| atomic_min(*p,val) | Read, store min(*p,val) Integers only |
| atomic_max(*p,val) | Read, store max(*p,val) Integers only |
| atomic_and(*p,val) | Read, store (*p & val) Integers only |
| atomic_or(*p,val) | Read, store (*p | val) Integers only |
| atomic_xor(*p,val) | Read, store (*p val) Integers only