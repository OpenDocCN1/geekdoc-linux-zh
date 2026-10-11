click the **Finish** button, the Connect to the Internet window (Figure 4-7) will appear. This is the same window that will appear any time you choose to connect to the Internet in the future.

![](bbox=[0.18, 0.11, 0.72, 0.31])

# Changing Your Dial-up Connection Settings from Pulse to Tone Dialing

There are two ways in which telephones transmit the numbers you dial when you try to call someone. The most common these days is tone dialing, which transmits the phone number you dial by means of tones. When you frequently dial a certain number, you probably have noticed that the number seems to have a distinct tune, which in fact it does. You might even have caught a mis dial at times when dialing a number because the tune for that phone number sounded wrong.

The other, increasingly less common, phone number transmission protocol is *pulse* dialing, which transmits the phone number you dial by means of pulses, one pulse for a 1, two pulses for a 2, and so on. If you have pulse dialing on your line, you will probably know it, because you can hear the pulses, or clicks, when you dial.

When you set up an Internet dial-up connection via the Connection Wizard, things are automatically set up for tone dialing. If you happen to have a line that requires pulse dialing, you will have to make a simple modification. To do this, open the Connect to the Internet window (Launch * Applications * Internet * Connect to the Internet), and click the **Properties** button. When the Properties window appears, click the **Protocol and Hardware** tab, and then click the **Properties** button in that tab.

In that Properties window, click the **Commands** tab, and then click directly on the word **ATDT** (to the right of *Dial*). The area directly surrounding the word will then transform into a text-input box, as you can see in Figure 4-8. In that box, change the current entry, **ATDT**, to **ATDP** (the last letter in “ATDT” is either T for tone or P for pulse), and then click **OK** in both of the open properties windows. After that, you’ll be ready to go.

# Connecting and Disconnecting Dial-up Connections

To get connected to the Internet via your dial-up connection, go to the Launch menu and select Applications * Internet * Connect to the Internet. After double-checking that your modem is on (if it is an external modem),