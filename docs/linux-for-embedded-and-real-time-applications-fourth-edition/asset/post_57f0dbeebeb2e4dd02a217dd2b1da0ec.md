
# Debugging embedded software

## Chapter Outline

- **Remote Debugging With Eclipse** 121
  - Remote Debug Launch Configuration 123
- **A Thermostat** 126
- **Host Workstation as Debug Environment** 127
  - Advanced Breakpoint Features 129
- **Debugger Services Framework** 132
  - Configuring Remote System Explorer 132
  - Debugging With Remote System Explorer 135
- **Resources** 137

> *If debugging is the process of removing bugs, then programming must be the process of putting them in.*
> *Edsger W. Dijkstra*

In Chapter 5, *Eclipse integrated development environment*, you saw how Eclipse integrates very nicely with the Gnu Debugger, GDB. In this chapter, we will look at additional features of GDB, and explore how to use GDB on our target board. We will also consider a simple approach to high-level simulation that can be useful in the early stages of development.

## Remote Debugging With Eclipse

In a typical desktop environment, the target program runs on the same machine as the debugger. But in our embedded environment, Eclipse with GDB runs on the host workstation and the program being debugged runs on the ARM target. You can think of GDB as having both a client and a server side, as illustrated in Fig. 8.1. The client is the user interface, and the server is the actual interaction with the program under test. GDB implements a serial protocol that allows the server and client sides to be separated and communicate either over an RS-232 link or Ethernet.

![](img/f03d6fa2c5faefc793771df52bbb2ef9_132_0.png)

**Figure 8.1**
Client/server nature of GDB.

There are two approaches to interfacing the target to the *gdb* serial protocol:

- **gdb stubs**. A set of functions linked to the target program. *gdb stubs* is an RS-232-only solution.
- **gdbserver**. This is a stand-alone program running on the target that, in turn, runs the program to be debugged. The advantage of *gdbserver* is that it is totally independent of the target program. In other words, the target builds the same regardless of remote debugging. Another advantage of *gdbserver* is that it runs over Ethernet. Finally, Eclipse uses *gdbserver*, so that is the best reason of all to use it.

*gdbserver* is part of the ARM cross-tool chain in `/usr/local/arm-unknown-linux-gnueabi`. It’s also already in the BBB’s root file system at `/usr/bin`.

To run the *measure* program under GDB, you would first `cd` to the `src/measure` directory and, as root user, execute:

```
gdbserver :10000 measure
```

The arguments to *gdbserver* are:

- Network port number preceded by a colon. The normal format is “host:port,” where “host” is either a host name or an IP address in the form of a dotted quad, but *gdbserver* ignores the host portion. The port number is arbitrary, as long as it does not conflict with another port number in use. Generally, port numbers below 1024 are reserved for established network protocols such as HTTP (port 80), so it is best to pick a number above 1023. Port number 10,000 happens to be the default for the Eclipse debugger.
- Target program name.
- Arguments to the target program, if any.

gdbserver responds with something like:

```
Process measure created; pid = 703
```

Your pid value may be different. This says that gdbserver has loaded the program, and is waiting for a debug session to begin on the specified port. You must be root user because the program is opening files for writing in /sys that are owned by root.

### Remote Debug Launch Configuration

We will need a different debug launch configuration for remote debugging. With the measure project selected in the Project Explorer view, bring up the Debug Configuration dialog either from Run > Debug Configurations..., or click the down arrow next to the cute little bug icon and select Debug Configurations... Even though there is a category called C/C++ Remote Application, we are going to create this new configuration under C/C++ Application just like we did for record_sort.

1. With C/C++ Application selected, click the New button. This brings up the Debug Configurations dialog, as we saw in Chapter 5, *Eclipse integrated development environment*, with the name and project entries filled out.
2. We need to fill in the C/C++ Application entry. Click Search Project... That brings up a dialog listing all of the executables found in the project. Select measure and click OK.
3. In the center of the dialog is an entry labeled Build (if required) before launching. I recommend selecting Disable auto build. There will be situations later on where auto build would try to build the all target and fail. The failure is innocuous, but it can be disconcerting. Note however that even if you disable auto build, Eclipse may still try to build the all target and output the following message:
   > Errors exit in the active configuration of project "measure". Proceed with launch?
   
   Click Yes. The debug session will proceed correctly.
4. At the bottom of the Main tab is an entry labeled Using GDB Debugger Services Framework (DSF) Create Process Launcher with a link labeled Select other... Click that link to bring up the dialog shown in Fig. 8.2.
5. Check Use configuration specific settings, and select Legacy Create Process Launcher. Click OK.

The issue here is how remote debug sessions are set up and controlled. DSF offers a more seamless, integrated “experience” that we will look at later in the chapter. For now, we will use the simpler approach offered by the Legacy Process Launcher.

![](img/f03d6fa2c5faefc793771df52bbb2ef9_134_0.png)

**Figure 8.2**
Launcher preference selection.

6. Now select the **Debugger** tab (Fig. 8.3). Since we are debugging **ARM** code, we need a version of **GDB** that understands **ARM** code. And we have to tell it we are debugging remotely.
7. In the **Debugger** drop-down, select `gdbserver`.
8. Be sure **Stop on startup at main** is checked.
9. In the **GDB Debugger** field enter `arm-linux-gdb`.
10. Select the **Connection** tab under **Debugger Options** (Fig. 8.4). For the **Type** drop-down, select **TCP**.
11. Enter the IP address of your BBB for the **Host name or IP address**.[^1] Now, click **Apply**.
12. If `gdbserver` is still waiting patiently on the target board, go ahead and click **Debug**. Otherwise, start up `gdbserver` as described earlier before clicking **Debug**.

Eclipse switches (or asks if you want to switch) to the **Debug** perspective. Even though you are now debugging on the target board, everything looks pretty much like it did when debugging `record_sort` on the workstation.

[^1]: “**Host**” is a little misleading here. It really refers to the target board.

![](img/f03d6fa2c5faefc793771df52bbb2ef9_135_0.png)

**Figure 8.3**
Debugger tab.

![](img/f03d6fa2c5faefc793771df52bbb2ef9_135_1.png)

**Figure 8.4**
Connection tab.

## A Thermostat

Let us move on to something a little more interesting, and potentially even useful. We will enhance the measure program by turning it into a “thermostat.” We will also take a look at using the host workstation as a preliminary testing environment.

We will have our thermostat activate a “cooler” when the temperature rises above a given setpoint, and turn the cooler off when the temperature falls below the setpoint. In practice, real thermostats incorporate hysteresis that prevents the cooler from rapidly switching on and off when the temperature is right at the setpoint. This is implemented in the form of a “deadband,” such that the cooler turns on when the temperature rises above the setpoint + deadband, and does not turn off until the temperature drops below setpoint − deadband. Additionally, the program includes an “alarm” that flashes if the temperature exceeds a specified limit.

Two of the LEDs will serve as the cooler and alarm respectively. These are defined in driver.h in the measure/ directory as COOLER and ALARM. The thermostat itself is fundamentally a simple state machine with three states based on indicated temperature:

- Normal
- High
- Limit

For each state, the action taken and next state are:

| Current State | Condition | Action | Next State |
| :--- | :--- | :--- | :--- |
| Normal | Temperature above setpoint + deadband | Turn on COOLER | High |
| Normal | Temperature above limit | Turn on ALARM | Limit |
| High | Temperature below setpoint − deadband | Turn off COOLER | Normal |
| High | Temperature above limit | Turn on ALARM | Limit |
| Limit | Temperature below limit | Turn off ALARM | |
