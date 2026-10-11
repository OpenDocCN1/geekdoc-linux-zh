```
```text
 18 /*
 19  * Define some primitives to manipulate sigset_t.
 20  */
 21
 22 #ifndef __HAVE_ARCH_SIG_BITOPS
 23 #include <asm/bitops.h>
 24
 25 /* We don't use <asm/bitops.h> for these because there is no need to
 26  * be atomic. */
 27 extern inline void sigaddset(sigset_t *set, int _sig)
 28 {
 29	    unsigned long sig = _sig - 1;
 30	    if (_NSIG_WORDS == 1)
 31		    set->sig[0] |= 1UL << sig;
 32	    else
 33		    set->sig[sig / _NSIG_BPW] |= 1UL << (sig % _NSIG_BPW);
 34 }
 35
 36 extern inline void sigdelset(sigset_t *set, int _sig)
 37 {
 38	    unsigned long sig = _sig - 1;
 39	    if (_NSIG_WORDS == 1)
 40		    set->sig[0] &= ~(1UL << sig);
 41	    else
 42		    set->sig[sig / _NSIG_BPW] &= ~(1UL << (sig % _NSIG_BPW));
 43 }
 44
 45 extern inline int sigismember(sigset_t *set, int _sig)
 46 {
 47	    unsigned long sig = _sig - 1;
 48	    if (_NSIG_WORDS == 1)
 49		    return 1 & (set->sig[0] >> sig);
 50	    else
 51		    return 1 & (set->sig[sig / _NSIG_BPW] >> (sig % _NSIG_BPW));
 52 }
 53
 54 extern inline int sigfindinword(unsigned long word)
 55 {
 56	    return ffz(~word);
 57 }
 58
 59 #define sigmask(sig)	    (1UL << ((sig) - 1))
 60
 61 #endif /* __HAVE_ARCH_SIG_BITOPS */
 62
 63 #ifndef __HAVE_ARCH_SIG_SETOPS
 64 #include <linux/string.h>
 65
 66 #define _SIG_SET_BINOP(name, op)	    \
 67 extern inline void name(sigset_t *r, const sigset_t *a, const sigset_t *b) \
 68 {					    \
 69	    unsigned long a0, a1, a2, a3, b0, b1, b2, b3;	\
 70	    unsigned long i;			    \
 71```
```