
selecting your video card you will be asked to select a video mode from a list of defaults. The resolution used is a matter of personal preference. The smaller the numbers are the larger the items on the display will be. Some combinations of video cards and video modes support virtual screens larger than the physical display. If your combination is one of these, you will be asked to select the virtual screen size.

## Mouse

Configuring your mouse with Metro-X requires that you know what type of mouse you have and how it is connected to your computer. When you select a mouse type, the default device will be provided in the configuration window. If you are in doubt, accept the default and make adjustments later if needed.

## Exiting

Selecting “Save and Exit” from the menu will save any changes you have made to the Metro-X configuration and exit the configX.curses program.

Selecting “Quit without Saving” from the menu will discard any changes you have made to the Metro-X configuration and exit the configX.curses program.

## 5.3.3 configX

Metro-X can also be configured for your system through a graphical utility called ConfigX, which is used to specify the mouse, keyboard, monitor, graphics card, color depth, and screen resolution(s) you are using.

## Start-up

- 1. Login as root and type the following command: /usr/bin/X11/configX
- 2. The explanation of special keys appears. (This message only appears prior to the initial configuration of Metro-X, when no Xconfig file exists.)
- 3. Press `Enter` to continue.

## Special Keys

When Metro-X is first installed, it doesn't yet recognize your mouse. Special keys must be used to move around the screens and make your selections during the initial configuration process.

| Key | Function |
| :--- | :--- |
| Tab | Moves forward from field to field. |
| Shift-Tab | Moves backward from field to field. |
| `↑` or `↓` or `←` or `→` | Changes the value in the current field. |
| Enter | Sets/unsets a toggle button. |
| Page Down | Switches to the next configuration page. |
| Page Up | Switches to the previous configuration page. |
| Esc | Cancels out of the current screen or pop-up. |
| Alt-F | Jumps to the File pull-down menu. |
| Alt-S | Jumps to the Screen pull-down menu. |
| Alt-C | Jumps to the Configuration pull-down menu. |

Figure 5.2: Function of Special Keys

## Mouse configuration

If the default mouse is not correct for your system:

- 1. Press `↓` to display the list of mice.
- 2. Press `↑` or `↓` to scroll to your mouse entry, then press `Enter` to select it.
- 3. Press `Tab` to move to the next field.
- 4. Press `↓` to display the list of mouse buttons. (The default entry is based on your mouse selection, and is usually the appropriate choice.)
- 5. Press `↑` or `↓` to scroll to your button entry, then press `Enter` to select it.
- 6. Press `Tab` to move to the next field.
- 7. If you need to change the path for your mouse device, edit it here.
- 8. Press `Tab` to move to the next field.

## Keyboard configuration

Metro-X includes international keyboard support, which allows you to select the keyboard appropriate for your language and country.

- 1. The initial keyboard setting is *Default: Default Console Mapping*, which will work with most keyboards.
- 2. Press `↓` to display the list of keyboards.
- 3. Press `↑` or `↓` to scroll to your keyboard entry, then press `Enter` to select it.
- 4. Press `Tab` to move to the next field.

## Monitor configuration

The default monitor setting is *Generic 640x480 @ 60Hz 13 inch*.

- 1. Press `↓` to display the list of monitors.
- 2. Press `↑` or `↓` to scroll to your monitor entry, then press `Enter` to select it.
- 3. Press `Tab` to move to the next field.
- 4. If you need to change the screen width (mm), edit it here.
- 5. Press `Tab` to move to the next field.
- 6. If you need to change the screen height (mm), edit it here.
- 7. Press `Tab` to move to the next field.

## Screen Saver

Some graphics cards and monitors support the Display Power Management System (DPMS), which minimizes the power used by the monitor when user input ceases. If your hardware has this feature, the phases of DPMS can be controlled in this section. The typical DPMS setup has a cascade effect, with the various phases being activated in succession with your choice of delay times between each.

- * X Screen Saver - Preliminary phase to DPMS, which blanks the screen but provides no power reduction.
- * Standby Mode - First phase of DPMS, which provides moderate power reduction by disabling the horizontal sync signal to the monitor.
- * Suspend Mode - Second phase of DPMS, which provides significant power reduction by disabling the vertical sync signal to the monitor.
- * Monitor Off - Final phase of DPMS, which provides maximum power reduction by disabling both the horizontal and vertical sync signals to the monitor.

- 1. In the *X Screen Saver* Delay field, press `Enter` to toggle this option on or off.
- 2. If toggled on, press `Tab` to move to the *Minutes* field, then use `←` or `→` to set the value.
- 3. Press `Tab` to move to the next field.
- 4. In the *Standby Mode* Delay field, press `Enter` to toggle this option on or off.
- 5. If toggled on, press `Tab` to move to the *Minutes* field, then use `←` or `→` to set the value.
- 6. Press `Tab` to move to the next field.
- 7. In the *Suspend Mode* Delay field, press `Enter` to toggle this option on or off.
- 8. If toggled on, press `Tab` to move to the *Minutes* field, then use `←` or `→` to set the value.
- 9. Press `Tab` to move to the next field.
- 10. In the *Monitor Off* Delay field, press `Enter` to toggle this option on or off.
- 11. If toggled on, press `Tab` to move to the *Minutes* field, then use `←` or `→` to set the value.

## Graphics Card Configuration

Press Page Down to move to the second configuration screen, which controls the graphics card, the number of colors, the virtual resolution, and the physical resolution.

Each graphics card configuration consists of five elements:

- * The graphics card (make and model).
- * The number of colors supported on screen simultaneously (color depth).
- * The virtual resolution of the screen (width x height).
- * The physical resolution of the screen (width x height).
- * The screen refresh rate (Hz).

Non-interlaced modes give a better screen appearance than refresh rates which are labeled "Interlaced". The highest refresh rate that your monitor supports will give the best image. At higher screen resolutions a higher refresh rate is particularly important to prevent the screen from visibly flickering. The highest refresh rate supported by the selected monitor is automatically displayed.

- 1. The default graphics card setting is IBM VGA.
- 2. Press `↓` to display the list of graphics cards.
- 3. Press `↑` or `↓` to scroll to your graphics card entry, then press `Enter` to select it.
- 4. Press `Tab` to move to the next field.

Not all graphics cards can support all color depths (number of colors). Only the options for the color depths supported by your card will be sensitive in this field. The other options will be greyed out.

- - Only *one* color option can be selected (due to design limitations of X).
- - In some cases the color options available will be limited by the physical resolution(s) you choose, based on the capabilities of your graphics card. Not all color depths are available at high resolutions.
- 1. The default setting is at the lowest value for your card.
- 2. Decide which available color setting you want to use.
- 3. Press `Tab` to move to that color setting, then press `Enter` to select it. (The previous setting will be cancelled.)
- 4. Press `Tab` to move to the next field.

The *Virtual Resolution* setting allows you to have an on-screen work area that is actually larger than your physical screen. Windows can extend beyond the screen's physical boundaries and are viewed by scrolling into the extended areas. Only the options for the virtual resolutions supported by your card will be sensitive in this field. The other options will be greyed out. If you don't want to use this feature, select the *Disabled* option.

- - Only *one* virtual resolution can be selected.
- - In some cases the virtual-resolution options available will be limited by the physical resolution(s) you choose, since the virtual resolution must always be greater than the highest physical resolution.
- 1. The default setting for virtual resolution is *Disabled*.
- 2. Decide which available virtual resolution you want to use.
- 3. Press `Tab` to move to that setting, then press `Enter` to select it. (The previous setting will be cancelled.)
- 4. Press `Tab` to move to the next field.
