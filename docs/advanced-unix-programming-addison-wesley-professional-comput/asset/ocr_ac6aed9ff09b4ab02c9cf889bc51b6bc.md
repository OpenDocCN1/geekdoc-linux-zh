# Error Handling

```
```c
#define EC_CLEANUP_END\\
)

#define ec_cmp(var, errrtn)\\
(\ 
    assert(!ec_in_cleanup); \
    if ((intptr_t)(var) == (intptr_t)(errrtn)) { \
        ec_push(__func__, __FILE__, __LINE__, #var, errno, EC_ERRNO);\\
        goto ec_cleanup_bgn; \
    })

#define ec_rv(var)\\
(\ 
    int errrtn; \
    assert(!ec_in_cleanup); \
    if ((errrtn = (var)) != 0) { \
        ec_push(__func__, __FILE__, __LINE__, #var, errrtn, EC_ERRNO);\\
        goto ec_cleanup_bgn; \
    })

#define ec_ai(var)\\
(\ 
    int errrtn; \
    assert(!ec_in_cleanup); \
    if ((errrtn = (var)) != 0) { \
        ec_push(__func__, __FILE__, __LINE__, #var, errrtn, EC_EAI);\\
        goto ec_cleanup_bgn; \
    })

#define ec_negl(x) ec_cmp(x, -1)
#define ec_null(x) ec_cmp(x, NULL)
#define ec_false(x) ec_cmp(x, false)
#define ec_eof(x) ec_cmp(x, EOF)
#define ec_nzero(x)\\
(\ 
    if (!((x) != 0)\\
        EC_FAIL)\
)

#define EC_FAIL ec_cmp(0, 0)
#define EC_CLEANUP goto ec_cleanup_bgn;
```
```

33