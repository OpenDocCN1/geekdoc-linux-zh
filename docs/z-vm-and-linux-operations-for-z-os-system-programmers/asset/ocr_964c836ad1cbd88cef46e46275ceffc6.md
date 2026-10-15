# Using the Operating System Messages panel

From the Hardware Management Console, you can use the Operating System Messages task (panel), which is the SYSC device, to log on to the OPERATOR user ID and view z/VM messages. You can also use the Operating System Messages panel to issue commands on the z/VM. This communication between the Hardware Management Console and z/VM is in line mode.

To use the Operating System Messages panel as the system operator console during the initial program load of the z/VM system, perform one of the following tasks (in the following list, refer to the named sections listed in z/VM: CP Planning and Administration, SC24-6083):

+   - Specify the CONS=SYSC IPL parameter when using the stand-alone program loader (SAPL). See "Passing IPL Parameters."
+   - Specify a load parameter of CONSSYSC to bypass the SAPL window and have the z/VM operator open on the Operator System Messages panel. See "Overriding Stand-Alone Program Loader Defaults."
+   - Add SYSTEM_CONSOLE to the OPERATOR_CONSOLES statement in the SYSTEM CONFIG file. See "System Configuration File."

To have emergency operating system messages displayed, add SYSTEM_CONSOLE to the EMERGENCY_MESSAGE_CONSOLES statement in the SYSTEM CONFIG file.

# Setting up and using the Integrated 3270 console

From the Hardware Management Console you can use the integrated 3270 console as the system operator's console. The integrated 3270 console is identified by z/VM as SYSG. This console provides you the ability to install, service, and operate z/VM without any attached 3270 devices. To identify the integrated 3270 console to CP during initial program load of the z/VM system, do one of the following tasks:

+   - Use the CONS=SYSG IPL parameter when using the stand-alone program loader (SAPL).
+   - Specify a load parameter of CONSSYSG to bypass the SAPL window and have the z/VM operator come up on the Integrated 3270 Console. See "Overriding Stand-Alone Program Loader Defaults" in z/VM: CP Planning and Administration, SC24-6083.
+   - Add SYSTEM_3270 to the OPERATOR_CONSOLES system configuration statement.

3 http://www.vm.ibm.com/pubs/hcsg0b01.pdf
4 http://www.vm.ibm.com/pubs/hcsg0b01.pdf