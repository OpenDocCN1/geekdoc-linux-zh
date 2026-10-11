# The Linux Scheduler

175

```
```
+++ 2.3.38-pset/kernel/sched.c Tue Jan 11 18:16:45 2000
@@ -72,11 +72,13 @@
 struct schedule_data {
        struct task_struct *curr;
        cycles_t last_schedule;
+	int bind;
 } schedule_data;
 char __pad [SMP_CACHE_BYTES];
 } aligned_data [NR_CPUS] __cacheline_aligned = { {&init_task,0}};
 #define cpu_curr(cpu) aligned_data[(cpu)].schedule_data.curr
+#define cpu_bind(cpu) (aligned_data[(cpu)].bind)
 struct kernel_stat kstat = { 0 };

@@ -94,6 +96,25 @@
 void scheduling_functions_start_here(void) { }
+static int not_deadlocking(void)
+{
+	int i;
+	for (i = 0; i < smp_num_cpus; i++) {
+	int cpu;
+	cpu = cpu_logical_map(i);
+	if (!cpu_bind(cpu))
+	return 1;
+	}
+return 0;
+
+void set_bind_cpu(int cpu, int set)
+{
+	cpu_bind(cpu_logical_map(cpu)) = set;
+
*/
 * This is the function that decides how desirable a process is..
 * You can weigh different processes against each other depending
@@ -111,6 +132,9 @@
static inline int goodness(struct task_struct * p, int this_cpu, struct mm_struct
*this_mm)
{
 int weight;
+	if (not_deadlocking() && cpu_bind(this_cpu) && p->bind_cpu != this_cpu)
+	return 0;
+	/*
+	Realtime process, select the first one on the
--- 2.3.38-pset/kernel/sys.c~1~ Tue Nov 2 12:06:25 1999
+++ 2.3.38-pset/kernel/sys.c Tue Jan 11 18:18:34 2000
```
```