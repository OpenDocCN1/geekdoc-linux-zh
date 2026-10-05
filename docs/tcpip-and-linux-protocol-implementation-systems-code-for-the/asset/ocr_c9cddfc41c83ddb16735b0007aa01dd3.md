# Forwarding 733

```
628   if (q || !tcm-tcm_handle && q-handle != !tcm-tcm_handle) {
629       if (tcm-tcm_handle) {
630          if (q && !(n-nmsg_flags&NLM_F_REPLACE)) {
631              return-EEXIST;
632          if (TC_H_MIN(tcm-tcm_handle)) {
633                  return-EINVAL;
634              if (q == qdisc_loop(dev, tcm-tcm_handle) == NULL) {
635                  goto create_n_graft;
636              if (n->nmsg_flags&NLM_F_EXCL) {
637                  return-EEXIST;
638              if (tca[TCA_KIND-i] && rtattstrcmp(tca[TCA_KIND-i], q->ops->id)) {
639                      return-EINVAL;
640                  if (q == p {
641                      (p && check_loop(q, p, 0)))
642                          return-ELOOP;
643                          atomic_inc(&q->refcnt);
644                  goto graft;
645
645 else {
```

Figure 9.106 Scheduler API–change queue discipline entry: linux/net/sched/sch_api.c.

```
646   if (q == NULL)
647       goto create_n_graft;
648
649   /* This magic test requires explanation.
650    * We know, that some child q is already
651      attached to this parent and have choice:
652      * either to change it or to create/graft new one.
653      * 1. We are allowed to create/graft only
654          if CREATE and REPLACE flags are set.
655    *
656      * 2. If EXCL is set, request wanted to say,
657          that qdisc_tcm_handle is not expected
658          and to exist, that we choose create/graft too.
659    *
660      * 3. The last case is when no flags are set.
661          Alas, it is sort of hole in API, we
662            cannot decide what to unambiguously.
663      * For now we select create/graft, if
664          user gave KIND, which does not matching.
665    *
666      if ((n->nmsg_flags&NLM_F_CREATE) &&
667          (n->nmsg_flags&NLM_F_REPLACE) &&
668              (n->nmsg_flags&NLM_F_EXCL) ||
669                  (tca[TCA_KIND-1])
670                      rtattstrcmp(tca[TCA_KIND-1], q->ops->id)))
671              goto create_n_graft;
672
673
674
675
} else {
```