After you have ensured your mouse is functioning properly, click the Keyboard tab and move to the next section to learn how to configure your keyboard.

# Keyboard Configuration Using XF86Setup

Keyboard configuration using XF86Setup is as easy as selecting the configuration of two combo boxes. Select the keyboard model from the Model combo box and the keyboard language from the Layout (language) combo box (see Figure 3.11). Click Apply to apply your settings. Most people do not need to set up the advanced functions on the right side of the screen because these are used to map keys for special keyboards.

FIGURE 3.11
Keyboard configuration using XF86Setup.

![](bbox=[0.28, 0.35, 0.65, 0.65])

# Card Configuration Using XF86Setup

Display card configuration using XF86Setup can be performed in the following two ways:

+   - **Detailed Setup**—Before using the detailed setup in Figure 3.12, you should have some knowledge of the X Window System servers. You should select the X server for your display card using the buttons at the top of the screen. You also should configure the appropriate settings for your X server. You can specify options for the X server using the Options combo box, which enables multiple selections. You can click the Card List button to select your card from a large list of cards, which takes less time than guessing which settings apply to your display card.
+   - **Card List**—In the Card List mode, all you have to do is to search for your display card in the card list (see Figure 3.13). After you have selected your card, you can move on to the next step or you can press the Detailed Setup button to add options to the settings that were applied when you selected the card.

> **NOTE** We recommend you specify the memory manually rather than making the X server probe for it. Use the Detailed Setup to specify the memory on your graphic card. In some graphic cards, you might have to turn on the software cursor if the cursor shape is missing while using X. To enable the software cursor, click the Options combo box and select sw_cursor. You should use this option only if the shape of your mouse cursor is not correct in X.