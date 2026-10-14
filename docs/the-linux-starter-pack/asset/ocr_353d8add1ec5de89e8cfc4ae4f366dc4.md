# Instant messaging

# Customising Pidgin

Now that you’ve got Pidgin working, it’s time to make it feel more like home.

# Quick tip

Buddy Pounce, found in the tool menu, will send a message to a contact as soon as they appear online.

There is a lot you can do to customise the Pidgin environment, but the first thing you should do is create an avatar for yourself. An avatar is an online representation of someone’s real-world character. These are seldom serious, and most people change them often to reflect their mood, adding some much-needed character to a world of text. It’s easy to create your own. First find an image you want to use – it needs to be square, and you might want to trim it slightly, as Pidgin offers no scaling options other than resizing. When you’ve found an image, click on the small icon in the bottom-right of the buddies list. This will open a file requester from where you can navigate to your image. After it’s selected, Pidgin will resize the image. Most protocols only use small images of 64x64 pixels, so your image needs to be easy to see. You can see it has replaced the original icon in the bottom-right of the buddies list, and it’s this image that people will see when they chat to you.

![](bbox=[0.565, 0.208, 0.895, 0.395])

There are loads of plugins to choose from – our favourite translates one language to another in real time.

# Plugins

The best way to add things to Pidgin is through its wonderful plugin system. If you’ve not come across plugins before, they’re separate modules that can be enabled to add functionality to an application. They’re left optional so that users can pick and choose which ones they prefer. It’s a little like adding extensions to Firefox, for instance. The plugins window is opened by selecting ‘Plugins’ from the ‘Tools’ menu. This window lists each plugin with an enable box to the left of a short description. Clicking on the enable box will start the plugin. Here are a few of our favourites:

+   » Auto-accept If someone sends you a file, you normally have to switch to the message window and accept the request. This plugin does it for you, downloading the file automatically without you having to do anything. You don’t need to worry about getting spammed with files, as only your contacts can send them.

+   » Buddy ticker If the vertical Buddies List takes up too much room, try the Buddy Ticker. It creates a sideways scrolling equivalent that takes up less room – your contacts slide across a narrow window on your screen, and you can use this list exactly like the normal window for starting conversations.

+   » Contact availability This is a clever plugin. It monitors what time of day your contacts are online so that it can estimate when they’re likely to be available. This is great for people in your contacts list who are in a different time zone, or people who only connect to the internet at certain times of the day.

+   » History This is an essential tool if you’ve got a lot of contacts. It shows the end of your previous conversation when you start a new one, so you can remember what you were both talking about. Even if you haven’t chatted to your buddy in weeks, the greyed out section of the conversation will show you your last mutterings.

# IM troubleshooting

Most instant messaging and VoIP problems are caused by firewalls blocking the ports necessary for one client to talk to another. This is because file transfers and chat use different ports. Opening the correct ports on your firewall isn’t always an easy job. If you’re not using a firewall you should have no problem, but if you are, you need to open ports on the firewall for the protocols you’re having problems with. MSN uses TCP port 1863, but if you use the HTTP option in Pidgin, it will use port 80. This is the same port that web browsers use, so it should definitely work. AIM uses TCP and UDP port 5190. Ekiga uses many different ports, and installing Stun (as requested by the install wizard) solves most connection problems. Most firewalls will have the option to enable common VoIP/SIP/Video Conferencing ports, and you should do this if you’re having problems. If your machine is connected to the internet through more than one router, this can also cause NAT problems. Try to create a direct route to each machine you want to use by creating static IP addresses and routes from one connection to the next. If your router has the facility, use NAT on your router to forward all VoIP ports to the machine you want to run Ekiga on.

![](bbox=[0.355, 0.685, 0.635, 0.82])

Many firewalls feature predefined rules for letting VoIP and instant messaging through.

+   » Psychic mode Pidgin knows when a contact starts to type a message to you. With this plugin enabled, it will open the message window before the message is even sent. You can tell when someone is typing because a small keyboard icon appears in the top-right of the chat window. This is essential when you’re both in full flow.

+   » Text replacement This plugin will replace certain strings you type in the message window with those you want them replaced with. This is useful for long words, or even for automatically correcting common mistakes. You might want to replace ‘youv’e’ with ‘you’ve’ for example, or replace a codeword with a long address.