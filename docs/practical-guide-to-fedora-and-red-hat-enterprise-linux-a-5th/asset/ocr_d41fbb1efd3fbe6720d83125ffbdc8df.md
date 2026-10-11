# # EXECUTING A COMMAND

**fork and sleep** When you give the shell a command, it usually *forks* (*spawns*) a child process to execute the command. While the child *process* is executing the command, the parent *process* *sleeps*. While a *process* is *sleeping*, it *does* not use any computer time but remains inactive, waiting to wake up. When the child *process* finishes executing the command, it tells its parent of its success or failure via its *exit* status and then *dies*. The parent *process* (which is running the *shell*) wakes up and prompts for another *command*.

**Background process** When you run a *process* in the background by ending a *command* with an *ampersand* (**&**), the *shell* *forks* a child *process* without *going* to *sleep* and without *waiting* for the child *process* to run to *completion*. The parent *process*, which is executing the *shell*, reports the *job* number and *PID* number of the child and *prompts* for another *command*. The child *process* runs in the *background*, *independent* of its *parent*.

**Builtins** Although the *shell* *forks* a *process* to run *most* of the *commands* you *give* it, some *commands* are *built* into the *shell*. The *shell* *does* not need to *fork* a *process* to run *builtins*. For more information refer to “*Builtins*” on *page* 247.

**Variables** Within a *given* *process*, *such* as *your* *login* *shell* or *a* *subshell*, you can *declare*, *initialize*, *read*, *and* *change* *variables*. By *default* *however*, *a* *variable* is *local* to *a* *process*. When *a* *process* *forks* *a* *child* *process*, *the* *parent* *does* *not* *pass* *the* *value* of *a* *variable* to *the* *child*. You *can* *make* *the* *value* of *a* *variable* *available* to *child* *processes* (*global*) by *using* the *export* *builtin* (*page* 926).

# # HISTORY

The *history* *mechanism*, *a* *feature* *adapted* *from* *the* C *Shell*, *maintains* *a* *list* of *recently* *issued* *command* *lines*, *also* *called* *events*, *providing* *a* *quick* *way* to *reexecute* *any* of *the* *events* in *the* *list*. This *mechanism* *also* *enables* you to *execute* *variations* of *previous* *commands* *and* to *reuse* *arguments* from *them*. You *can* *replicate* *complicated* *commands* *and* *arguments* that you *used* *earlier* in *this* *login* *session* or in *a* *previous* *one* *and* *enter* *a* *series* of *commands* that *differ* from *one* *another* in *minor* *ways*. The *history* *list* *also* *serves* as *a* *record* of *what* you *have* *done*. It *can* *prove* *helpful* when you *have* *made* *a* *mistake* *and* are *not* *sure* *what* you *did* or *when* you *want* to *keep* *a* *record* of *a* *procedure* that *involved* *a* *series* of *commands*.

The *history* *builtin* *displays* the *history* *list*. If it *does* *not*, *read* on—you *need* to *set* *some* *variables*.

# # VARIABLES THAT CONTROL HISTORY

The *value* of *the* **HISTSIZE** *variable* *determines* *the* *number* of *events* *preserved* in *the* *history* *list* *during* *a* *session*. A *value* in *the* *range* of *100* to *1,000* is *normal*.

When you *exit* *from* *the* *shell*, *the* *most* *recently* *executed* *commands* *are* *saved* in *the* *file* *given* by *the* **HISTFILE** *variable* (*the* *default* is *~/.bash_history*). The *next* *time* you *start* *the* *shell*, *this* *file* *initializes* the *history* *list*. The *value* of *the* **HISTFILESIZE**