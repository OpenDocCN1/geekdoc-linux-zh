![](bbox=[0.13, 0.08, 0.81, 0.4])

# Monitoring power usage on laptop computers

To effectively use a laptop computer, you need to be able to monitor and manage the laptop’s power usage. Using tools provided in Fedora, you can configure your laptop to:

+   - Monitor the battery level.
+   - Notify you when the battery is low.
+   - Notify you when the battery is fully charged.
+   - Show when the laptop is plugged in.
+   - Suspend the current session.

Fedora offers two facilities that do power management: APM and ACPI.

+   - **Advanced Power Management (APM)** — APM can be used to monitor the battery of your notebook and notify user-level programs to tell you when your battery is low. It can also be used to place your laptop into suspend mode.
+   - **Advanced Configuration and Power Interface (ACPI)** — Besides monitoring power features on your laptop, ACPI can also do thermal control, motherboard configuration, and change power states.

Many older laptops do not include support for ACPI in the BIOS, so you must use APM to monitor and manage your batteries. For some newer laptops, ACPI may be required. In general, ACPI offers a more complete feature set for power management, but APM has more user-level support today.