The location of your own panic function has little importance, but the registration of this function must be done during system initialization. In our case, we add a *mypanic.c* file in the *kernel* directory of the kernel sources and modify that directory's *Makefile* accordingly. Here is the *mypanic.c* for our control module:

```
```c
#include <linux/kernel.h>
#include <linux/init.h>
#include <linux/notifier.h>

static int my_panic_event(struct notifier_block *,
                          unsigned long,
                          void *);

static struct notifier_block my_panic_block = {
   notifier_call:  my_panic_event,
   next:           NULL,
   priority:       INT_MAX
};

int _ _init register_my_panic(void)
{
   printk("Registering buzzer notifier \n");
   notifier_chain_register(&panic_notifier_list,
                           &my_panic_block);
   return 0;
}

void ring_big_buzzer(void)
{
   ...
}

static int my_panic_event(struct notifier_block *this,
                          unsigned long event,
                          void *ptr)
{
   ring_big_buzzer();
   return NOTIFY_DONE;
}

module_init(register_my_panic);
```
```

The *module_init(register_my_panic);* statement ensures that the *register_my_panic* function is called during the kernel’s initialization without requiring any modification of the kernel’s startup functions. The registration function adds *my_panic_block* to the list of other blocks in the panic notifier list. The *notifier_block* structure has three fields. The first field is the function to be called, the second is a pointer to the next notifier block, and the third is the priority of this block. In our case, we want to have the highest possible priority. Hence the use of *INT_MAX*.