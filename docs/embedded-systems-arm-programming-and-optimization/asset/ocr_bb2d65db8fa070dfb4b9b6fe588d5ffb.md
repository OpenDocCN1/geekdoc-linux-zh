# 234 APPENDIX A Adding PMU Support to Raspian for the Generation 1 Raspberry Pi

command to download a specific branch of the source code using a command as:

```
git clone-branch rpi-3.12.y
https://github.com/raspberrypi/linux.git
```

You can download the ARM cross-compiler toolchain for Intel-based workstations at https://github.com/raspberrypi/tools.git.

# A.2 KERNEL MODIFICATIONS

In the kernel source code, open the file arch/arm/bcm2708/bcm2708.c. At (or around) line 468, add the following code:

```
static struct platform_device bcm2708_pmu_device = {
    .name = "arm-pmu",
    .id = -1, /* Only one */
};

```

In the function bcm2708_init(), after the following line of code:

```
bcm_register_device(&bcm2708_powerman_device);
...:add:
```

```
bcm_register_device(&bcm2708_pmu_device);
```

Next, open the file arch/arm/kernel/perf_event_cpu.c. In the cpu_pmu_request_irq(1) function, change the following code:

```
if (irqs < 1) {

    pr_err("no irqs for PMUs defined\n");

    return -ENODEV;
}
```

...to:

```
if (irqs < 1) {

    printk_once("no irqs for PMUs defined, disabling sampled events\n");

    return 0;
}
```