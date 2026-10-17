
```c
 */

#ifndef __HAVE_ARCH_SIG_BITOPS

#include <asm/bitops.h>

/* 我们这里不使用 <asm/bitops.h>，因为不需要原子性。 */

extern inline void sigaddset(sigset_t *set, int _sig)

{

    unsigned long sig = _sig - 1;

    if (_NSIG_WORDS == 1)

            set->sig[0] |= 1UL << sig;

    else

            set->sig[sig / _NSIG_BPW] |= 1UL << (sig % _NSIG_BPW);

}

extern inline void sigdelset(sigset_t *set, int _sig)

{

    unsigned long sig = _sig - 1;

    if (_NSIG_WORDS == 1)

            set->sig[0] &= ~(1UL << sig);

    else

            set->sig[sig / _NSIG_BPW] &= ~(1UL << (sig % _NSIG_BPW));

}

extern inline int sigismember(sigset_t *set, int _sig)

{

    unsigned long sig = _sig - 1;

    if (_NSIG_WORDS == 1)

            return 1 & (set->sig[0] >> sig);

    else

            return 1 & (set->sig[sig / _NSIG_BPW] >> (sig % _NSIG_BPW));

}

extern inline int sigfindinword(unsigned long word)

{

    return ffz(~word);

}

#define sigmask(sig)            (1UL << ((sig) - 1))

#endif /* __HAVE_ARCH_SIG_BITOPS */

#ifndef __HAVE_ARCH_SIG_SETOPS

#include <linux/string.h>

#define _SIG_SET_BINOP(name, op)            \
extern inline void name(sigset_t *r, const sigset_t *a, const sigset_t *b) \
{                                            \
    unsigned long a0, a1, a2, a3, b0, b1, b2, b3;    \
    unsigned long i;                \
    for (i = 0; i < _NSIG_WORDS/4; ++i) { \
        a0 = a->sig[4*i+0]; a1 = a->sig[4*i+1]; \
        a2 = a->sig[4*i+2]; a3 = a->sig[4*i+3]; \
        b0 = b->sig[4*i+0]; b1 = b->sig[4*i+1]; \
        b2 = b->sig[4*i+2]; b3 = b->sig[4*i+3]; \
        r->sig[4*i+0] = op(a0, b0); \
        r->sig[4*i+1] = op(a1, b1); \
        r->sig[4*i+2] = op(a2, b2); \
        r->sig[4*i+3] = op(a3, b3); \
    } \
    switch (_NSIG_WORDS % 4) { \
        case 3: \
            a0 = a->sig[4*i+0]; a1 = a->sig[4*i+1]; a2 = a->sig[4*i+2]; \
            b0 = b->sig[4*i+0]; b1 = b->sig[4*i+1]; b2 = b->sig[4*i+2]; \
            r->sig[4*i+0] = op(a0, b0); \
            r->sig[4*i+1] = op(a1, b1); \
            r->sig[4*i+2] = op(a2, b2); \
            break; \
        case 2: \
            a0 = a->sig[4*i+0]; a1 = a->sig[4*i+1]; \
            b0 = b->sig[4*i+0]; b1 = b->sig[4*i+1]; \
            r->sig[4*i+0] = op(a0, b0); \
            r->sig[4*i+1] = op(a1, b1); \
            break; \
        case 1: \
            a0 = a->sig[4*i+0]; b0 = b->sig[4*i+0]; \
            r->sig[4*i+0] = op(a0, b0); \
            break; \
    } \
}

#define _sig_or(x,y)      ((x) | (y))

_SIG_SET_BINOP(sigorsets, _sig_or)

#define _sig_and(x,y)     ((x) & (y))

_SIG_SET_BINOP(sigandsets, _sig_and)

#define _sig_nand(x,y)    ((x) & ~(y))

_SIG_SET_BINOP(signandsets, _sig_nand)

#undef _SIG_SET_BINOP

#undef _sig_or

#undef _sig_and

#undef _sig_nand

#define _SIG_SET_OP(name, op) \
extern inline void name(sigset_t *set) \
{ \
    unsigned long i; \
    for (i = 0; i < _NSIG_WORDS/4; ++i) { \
        set->sig[4*i+0] = op(set->sig[4*i+0]); \
        set->sig[4*i+1] = op(set->sig[4*i+1]); \
        set->sig[4*i+2] = op(set->sig[4*i+2]);

        set->sig[4*i+3] = op(set->sig[4*i+3]);\
    }\
    switch (_NSIG_WORDS & 4) {\
    case 3: set->sig[4*i+2] = op(set->sig[4*i+2]);\
        case 2: set->sig[4*i+1] = op(set->sig[4*i+1]);\
            case 1: set->sig[4*i+0] = op(set->sig[4*i+0]);\
    }\
}

#define _sig_not(x)         (~(x))

_SIG_SET_OP(signotset, _sig_not)

#undef _SIG_SET_OP

#undef _sig_not

extern inline void sigemptyset(sigset_t *set)

{

    switch (_NSIG_WORDS) {

    default:

        memset(set, 0, sizeof(sigset_t));

        break;

    case 2: set->sig[1] = 0;

        case 1: set->sig[0] = 0;

            break;

    }

}

extern inline void sigfillset(sigset_t *set)

{

    switch (_NSIG_WORDS) {

    default:

        memset(set, -1, sizeof(sigset_t));

        break;

    case 2: set->sig[1] = -1;

        case 1: set->sig[0] = -1;

            break;

    }

}
```
