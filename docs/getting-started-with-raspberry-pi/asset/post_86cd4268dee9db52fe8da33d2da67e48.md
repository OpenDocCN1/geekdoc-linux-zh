
{0x1},
};

MODULE_DEVICE_TABLE(pci, i855_pci_tbl);

/* pci_driver structure for this device.
   Re-visit Chapter 10 for a detailed explanation */
static struct pci_driver i855_driver = {
    .name         = "855",
    .probe        = i855_probe,
    .remove       = __devexit_p(i855_remove),
    .id_table     = i855_pci_tbl,
};

/* Driver Initialization */
static int __init
i855_init(void)
{
    /* ... */
    pci_rc = pci_register_driver(&i855_driver);
    /* ... */
}

Look at `drivers/edac/` for EDAC source files and at `Documentation/drivers/edac/edac.txt` for detailed semantics of EDAC sysfs nodes.

## Frequency Scaling

The CPU frequency (`cpufreq`) driver subsystem aids power management by scaling CPU frequencies on-the-fly. If you use a suitable scaling algorithm (called a `governor`), your device's battery can potentially last longer. Cpu-freq supports several architectures such as x86, ARM, and PowerPC. To obtain cpufreq capabilities, you also need to enable a suitable processor driver (say, the Intel Enhanced SpeedStep driver if you are using a SpeedStep-enabled CPU such as Pentium M).

You can control cpufreq's behavior via files in the `/sys/devices/system/cpu/cpuX/cpufreq/` directory, where X is the CPU number. To set maximum and minimum frequency scaling limits, write desired values to `scaling_max_freq` and `scaling_min_freq`, respectively. To see a list of supported cpufreq governors, look at the contents of `scaling_available_governors`. The kernel supports several governors:

- `Performance` governor statically sets the CPU frequency to `scaling_max_freq`.
- `Powersave` sets the CPU frequency to `scaling_min_freq`.
- `Ondemand` adjusts the frequency depending on CPU load.
- `Conservative` is a variant of ondemand where the speed change occurs smoothly in gradual steps.
- `Userspace` lets applications dictate the scaling technique. Some distributions set the governor to userspace and implement the scaling algorithm via a daemon called `cpuspeed`, which is spawned during boot.
- You may also implement your own kernel governor using the `cpufreq_register_governor( )` interface.

Each supported governor is implemented as a kernel module. To see cpufreq in action, assign a governor and vary the system load:

```bash
bash> cd /sys/devices/system/cpu/cpu0/cpufreq
bash> cat scaling_max_freq  # Maximum frequency
1700000
bash> cat scaling_min_freq  # Minimum frequency
600000
bash> cat cpuinfo_cur_freq  # Current frequency
600000
bash> cat scaling_governor  # Scaling algorithm in use
powersave
bash> cat scaling_available_frequencies
1700000 1400000 1200000 1000000 800000 600000
bash> cat scaling_available_governors
conservative ondemand powersave userspace performance
bash> echo conservative > scaling_governor
# Assign 'conservative' governor
bash> ls -1R /
# Switch to another terminal and
# load your system by recursively listing all directories
```

If you now monitor the running frequency by looking at `/sys/devices/system/cpu/cpu0/cpufreq/cpuinfo_cur_freq`, you will see it dancing to the tune of the CPU load.

The CPU scaling code lives in the `drivers/cpufreq/` directory. Look at `Documentation/cpu-freq/` for the detailed semantics of cpufreq sysfs nodes.

## Embedded Controllers

Notebook computers and their derivatives usually contain a built-in `embedded controller` (EC) to take care of various side responsibilities, including the following:

- Interfacing with the keyboard controller
- Managing thermal events
- Handling special buttons and LEDs
- Controlling system and CPU fan speeds
- Monitoring battery voltage

Most of these functions are specific to the OEM’s hardware implementation. Different OEMs use different ECs; IBM/Lenovo laptops, for example, embed a Renesas H8 microcontroller to assist the main processor. The interface to access the EC, however, is standard irrespective of the make of the controller. The BIOS and the operating system operate on I/O port `0x80` to read information from the EC and I/O port `0x81` to write data to the EC. On desktops, these ports provide access to the keyboard controller rather than to a general-purpose EC.

The next section refers to an example driver that detects telemetry strength by accessing EC memory space.

## ACPI

*Advanced Configuration and Power Interface* (ACPI) is a power-management specification that replaces earlier standards such as *Advanced Power Management* (APM). ACPI is responsible for transitioning the system between power states. It also has the task of interfacing with devices and sensors connected to the EC. Such devices are called *ACPI devices*, and memory devoted to handle them is called *ACPI space*.

As you saw elsewhere in this book, low-level code is not the place to implement policy. This was the main problem with APM, where most of the power-management policies were part of BIOS firmware. ACPI shifts policy one level up, to the operating system. Using a daemon called *acpid*, ACPI even allows policy to be pushed one more level up, to user-space configuration files. By adding rules to an *acpid* configuration file, you can decide what to do when a hotkey is pressed or when a thermal trip occurs.

Even with ACPI, low-level BIOS firmware retains the responsibility of interfacing with hardware and detecting ACPI events such as a power button press or a thermal sensor report. To perform this, the BIOS utilizes a special x86 execution mode triggered via *system management interrupts* (SMIs). The SMI execution mode is transparent to the operating system. To notify the operating system about ACPI events detected in SMI mode, the BIOS asserts a *system control interrupt* (SCI). Look at `drivers/acpi/osl.c` for the Linux ACPI code that requests the SCI IRQ.

Linux ACPI components include the following:

1. A core layer that provides ACPI essentials such as the *ACPI Machine Language* (AML) interpreter. ACPI-specific BIOS code is written in AML, a language that runs on a virtual machine implemented by the operating system’s AML interpreter.

2. ACPI drivers for interfacing with standard components such as the EC (`drivers/acpi/ec.c`), buttons (`drivers/acpi/button.c`), and fan (`drivers/acpi/fan.c`). OEM-specific drivers offer support for features not supported by the standard ACPI drivers. For example, `drivers/mics/thinkpad_acpi.c` [1] is the OEM-specific driver that implements extras for IBM/Lenovo Thinkpads. On an IBM/Lenovo Thinkpad, the files under `/proc/acpi/` are generated by the standard ACPI drivers, whereas those in `/proc/acpi/ibm/` are produced by the OEM-specific driver. So, to get the current temperature, do this:

```bash
bash> cat /proc/acpi/thermal_zone/THM0/temperature
temperature:         39 C
```

But to turn on the nightlight on top of the LCD display, get help from the OEM-specific driver:

```bash
bash> echo on > /proc/acpi/ibm/light
```

3. A kernel thread `kapcid` that ACPI uses to queue work for execution.

4. Individual device drivers that use ACPI’s services to respond to transitions in the system’s power state. To achieve this, drivers register `suspend()` and `resume()` methods to the kernel’s device model. We alluded to these methods while discussing the `platform_driver` structure in Chapter 6, “Serial Drivers,” the `spi_driver` structure in Chapter 8, “The Inter-Integrated Circuit Protocol,” the `pci_driver` structure in Chapter 9, “PCMCIA and Compact Flash,” and the `pci_driver` structure in Chapter 10.

[1] Prior to 2.6.22, this driver used to be `drivers/acpi/ibm_acpi.c`.

5. User-space tools such as `acpitool`, which report the state of various ACPI devices, show thermal zone information and suspend the system to different sleep states:

```bash
bash> acpitool
Battery #1	: charging, 69.08%, 01:14:02
AC adapter	: on-line
Thermal zone 1: ok, 38 C
```

6. The `acpid` daemon, which is the policy enabler for ACPI events. It listens on `/proc/acpi/events` for power-management events reported by the kernel. When you press the power button or when a thermal trip occurs, the kernel ACPI driver dispatches an event to user space via `/proc/acpi/events`. Acpid reads this, passes it through configuration scripts present in `/etc/acpi/events/` and takes specified actions. Assume that you want to execute a specific program (`/bin/lidhandler`) when your laptop's lid button is pressed. For this, add the following to `/etc/acpi/events/acpi_handler.sh`:

```
event=button/lid,*
action=/bin/lidhandler
```

You may use `cpufreq` in tandem with ACPI. You can, for example, add this line inside `/bin/lidhandler` to drop down the processor frequency when you shut your laptop's lid:

```
echo powersave > /sys/devices/system/cpu/cpu0/cpufreq/scaling_governor
```

You can download the ACPI specifications from www.acpi.info.

As an exercise, consider that you have a telemetry card[2] built in to an embedded laptop derivative, and that the EC is connected to a sensor that measures telemetry strength. To access telemetry strength via `/proc/acpi/` (or `/sys/bus/acpi/`), update the corresponding laptop model's "extras" driver present in `drivers/misc/`. If your board is a derivative of an IBM/Lenovo Thinkpad, for example, modify `drivers/misc/thinkpad_acpi.c` accordingly. You may use the `ec_read()` and `ec_write()` kernel functions to access the location that stores telemetry strength in the EC's ACPI space.

[2] We developed a driver for an example telemetry card in Chapter 11, "Universal Serial Bus."
