# Build a VoIP server

![](bbox=[0.09, 0.08, 0.46, 0.35])

# Trying it out

07 If you're using an Android OS phone, we recommend CspSimple, which can be found on Google Play. We recommend LyncPhone for Linux clients. Well use two Android phones as an example. When adding an account in CspSimple, scroll down to the Generic wizards section and select Basic. Then fill in the information as shown in the image below. Once you have two devices set up, try calling between the two.

![](bbox=[0.69, 0.31, 0.99, 0.61])

# The web interface

03 Type the static IP address of your Raspberry Pi into a web browser. You'll be taken to the FreePBX web interface for configuring Asterisk. Click the FreePBX Administration button and use the username 'admin' and password 'admin'. The User Control Panel allows users to listen to their voicemails.

# Add a conference extension

![](bbox=[0.41, 0.46, 0.65, 0.55])

# Add extensions

04 Each device that will be connected needs its own extension. To add an extension, hover over the Applications tab, then select Extensions. Select Generic SIP Device as the device type and click Submit. The User Extension is the number to call to get to that device. The Display Name can either be the name of a person or just the same as the User Extension. The one other thing that you will need to fill in is the secret, which is a passphrase that allows the device to connect. One of these will have been generated, but you can change it if you like. Scroll to the bottom and click Submit. Add as many extensions as you like.

05 Go to the Applications section and select Conferences. Choose a number and name for the conference, and a PIN number if you'd like users to require a PIN to join. Click Submit Changes once you've done.

# Apply config

06 Changes such as adding extensions and conferences are not made until the Apply Config button is pressed, so be sure to do that before closing the web interface.

# Trying a conference call

08 Call the conference number from the devices you set up from one of the PIN code you'll need to follow by the # key. You'll be told that you are the only person in this conference, and will hear a notification whenever anyone else joins and leaves the conference.

> "Each client gets a phone number and can call other clients. You can also have conference calls"