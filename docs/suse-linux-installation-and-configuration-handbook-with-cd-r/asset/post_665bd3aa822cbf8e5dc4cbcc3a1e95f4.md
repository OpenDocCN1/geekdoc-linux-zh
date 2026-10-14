
Luckily, SuSE Linux includes a YaST module that configures WvDial. The next section explains how to configure WvDial manually and by using the YaST module.

## Configuring WvDial Using YaST

You can use YaST to configure a modem connection without having to go through the trouble of editing files and configuring devices. YaST uses interactive menus to set up a connection from the ground up. To set up a connection using YaST, follow these steps:

- 1. Start YaST.
- 2. Open System Administration, Network Configuration, Configure a PPP Network. This will bring up the SuSE WvDial Configuration window (see Figure 23.3).

### FIGURE 23.3
SuSE WvDial Configuration window.

![](img/659f91d9da7b29976c0625e2e9628511_444_0.png)

### SuSE WvDial Configuration

The first step in WvDial configuration is to configure it to detect your modem. To do so, highlight the Autodetect Modem option and press Enter. WvDial will attempt to scan your serial ports looking for a modem. After it finds one, WvDial will attempt to communicate with the modem and find the best init and dial strings to use with the modem. Scroll down the output window to check the output of the wvdialconf program.

Next, you must edit the connection profile by highlighting the Configure the Current Profile option and pressing Enter. Once in the Configure the Current Profile menu, fill in the following values (see Figure 23.4):

- - Phone number—Your ISP phone number.
- - Area code—The area code of your ISP. You can leave this field empty if you are dialing from the same area.
- - Account name—The username you use to connect to this ISP.
- - Password—Your password.

### FIGURE 23.4

You can configure the new connection using the Current Profile Window.

![](img/659f91d9da7b29976c0625e2e9628511_445_0.png)

Automatic DNS—Check this box if your DNS supplies you with the DNS when you connect.

Dial method—Select the dialing method from Tone dial or Pulse dial.

Modem on PBX (no dialtone)—Check this box if your modem is on a PBX or you get an error saying there is no dialtone. Note that your modem will not complain if the phone line is not connected if you check this box.

Authentication mode—Select the authentication mode your ISP uses. WvDial recognizes most of the authentication modes used by many ISPs. You have the following options:

- - PAP/CHAP
- - Compuserve
- - Germany:T-Online
- - Non-Standard Login

Expert menu—Using this menu, you can change the type of modem you are using (see Figure 23.5). You can also change the init strings that are sent to the modem when initializing the modem.

### FIGURE 23.5

Using the Expert menu, you can set up the modem type and modem advanced settings.

![](img/659f91d9da7b29976c0625e2e9628511_446_0.png)

- - Init String 2—This string will be sent to the modem when WvDial receives an OK reply for the first initialization string.
- - Serial port—If WvDial failed to correctly detect your modem port, you can specify it manually using this field.
- - Baud rate—You can edit the default baud rate you want to use in this field.

If your ISP does not assign you a DNS automatically, you should configure the DNS by highlighting the Configure DNS with YaST (Only if not Auto DNS) option and pressing Enter. This will bring up the YaST DNS configuration, which was discussed previously in the section “Setting Up YaST (Domain Name Server).”

After you have finished configuring WvDial, test your new connection by highlighting the Run WvDial option and pressing Enter. If your connection goes flawlessly, press Esc. You will be prompted to save your settings. Save your settings and exit.

Later, when you want to establish a connection, enter the following command:

```
bash$wvdial
```

Your modem will start dialing your ISP and establish a connection.

## Configuring WvDial Manually

To configure wvdial, you must log in to X session (through xdm or startx). After you're inside X, start an xterm and follow these steps:

- 1. Enable connectivity to the X server from the localhost by issuing the following command in an xterm:
- xhost +localhost
- 2. Change to a superuser, such as the following:
- su -l

3. Issue the following command:

```
wvdialconf /etc/wvdial.conf
```

You should get output that looks like this:

```
bash# wvdialconf /etc/wvdial.conf
Scanning your serial ports for a modem.

Port Scan<*1>: Ignoring ttyS0 because /dev/mouse is a link to it.
ttyS1<*1>: AT -- AT -- AT -- nothing.
ttyS2<*1>: AT -- OK
ttyS2<*1>: ATZ -- OK
ttyS2<*1>: ATQ0 -- OK
ttyS2<*1>: ATQ0 V1 -- OK
ttyS2<*1>: ATQ0 V1 E1 S0=0 -- OK
ttyS2<*1>: ATQ0 V1 E1 S0=0 &C1 -- OK
ttyS2<*1>: ATQ0 V1 E1 S0=0 &C1 &D2 S11=55 -- OK
ttyS2<*1>: ATQ0 V1 E1 S0=0 &C1 &D2 S11=55 +FCLASS=0 -- OK
ttyS2<*1>: Modem Identifier: ATI -- 33600
ttyS2<*1>: Speed 2400: AT -- OK
ttyS2<*1>: Speed 4800: AT -- OK
ttyS2<*1>: Speed 9600: AT -- OK
ttyS2<*1>: Speed 19200: AT -- -- OK
ttyS2<*1>: Speed 38400: AT -- OK
ttyS2<*1>: Speed 57600: AT -- -- OK
ttyS2<*1>: Speed 115200: AT -- OK
ttyS2<*1>: Speed 230400: AT -- OK
ttyS2<*1>: Max speed is 230400; using 115200 to be safe.
ttyS2<*1>: ATQ0 V1 E1 S0=0 &C1 &D2 S11=55 +FCLASS=0 -- OK

Found a modem on /dev/ttyS2.
ttyS2<Info>: Speed 115200; init "ATQ0 V1 E1 S0=0 &C1 &D2 S11=55 +FCLASS=0"
+FCLASS=0"
```

With this, wvdialconf has found your modem, guessed the dial string, guessed the speed, and wrote the corresponding configuration file.

- 4. Export the DISPLAY of the super user to be equal to the current X session, for example:
- export DISPLAY=:0
- 5. Start wdial.tcl and fill in the information in the configuration dialog box (see Figure 23.6).
- 6. Press Save to save the current configuration file. You can also click Dial to test the connection. If it says you have a connection, skip ahead to the section "Testing an Existing Connection."

The next time you try to connect, you'll have to open a terminal or a normal console and start wvdial. To disconnect, activate the window/console and press Ctrl+C.

### FIGURE 23.6
The wvdial.tcl script. Using this script makes it easy to modify the wvdial configuration file.

![](img/659f91d9da7b29976c0625e2e9628511_448_0.png)

## Using minicom

minicom is considered one of the main programs for testing and troubleshooting modems. In fact, you might find yourself using minicom in cases where you find your modem stuck and unable to hang up, or you might use it as your main dial-in program. When you first start minicom, you should start it as root with the -s parameter (see Figure 23.7). This parameter brings up the setup menu for minicom in which you should specify the serial port to be used for the modem.

### FIGURE 23.7
Starting minicom with the -s command-line parameter brings up the configuration screen for minicom.

![](img/659f91d9da7b29976c0625e2e9628511_448_1.png)

As noted before, the serial port of the modem has become /dev/modem. You might want to change the Modem and Dialing settings to suit your modem configuration, in which case you will be referring to your modem manual. After you've finished setting up minicom, you should save the settings. By saving the settings, minicom will change to the terminal screen at which you can send commands directly to the modem or bring up minicom facilities.

You can look up the mini modem commands in Table 23.5. The minicom help dialog box can be brought up by Alt+Z, which shows a menu with the available commands.

To establish a connection using minicom, use the following steps:

- 1. Press Alt+D to bring up the dialing directory.
- 2. Press Add by moving the cursor using the left and right arrows.
- 3. Select the new entry using the up and down arrows (see Figure 23.8)

### FIGURE 23.8

Adding a new entry in the minicom dialing directory.

![](img/659f91d9da7b29976c0625e2e9628511_449_0.png)

4. Press Edit.

5. Change the entries applicable as follows (see Figure 23.9):

- - A—Name of connection
- - B—Phone number
- - C—Dialing script number

### FIGURE 23.9

Editing the proper entries in the new connection.

![](img/659f91d9da7b29976c0625e2e9628511_449_1.png)

minicom can automate a connection, but this is not explained in this chapter. Refer to the minicom manual for more information about automating a connection using scripts.
