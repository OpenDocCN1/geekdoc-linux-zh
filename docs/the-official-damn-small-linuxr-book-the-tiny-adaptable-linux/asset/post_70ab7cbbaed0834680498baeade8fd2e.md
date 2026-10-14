
Both sides can begin typing messages, with the results looking like the window shown in Figure 14-7.

![](img/af53325d7f38f1cdafca9f44568e4ab8_306_0.png)

FIGURE 14-7 Open an instant message window to chat with another Skype contact.

You can add other contacts to the chat by selecting the Add More Users to This Chat button. Then, you can choose people from your contacts list to add as chat participants. The result is that the users you choose are asked to participate.

During the chat, you have many of the features available that you would expect to see during a chat session. For example, you can change the chat topic or select to bookmark the chat.

## USING SKYPE FOR-PAY SERVICES AND PRODUCTS

Before you can start making local, national, or international calls from Skype to phones on the standard telephone system, you need to pay for one of the Skype programs that let you do that. Other purchases you can make from Skype include wireless phones and other telephone hardware. Check the Skype website (http://skype.com/products) to learn about the different products available from Skype.

### Purchasing Calling Time

Because these programs change often, you need to check the Skype website for the latest programs and pricing. However, at the time of this writing, here are some of the available telephone calling programs:

- **SkypeOut**—This program lets you make calls from your computer to phones and mobile devices on the traditional phone system. There are yearly rates for unlimited calls within the United States and Canada (currently $29.95 per year). For international calls, there are per minute rates offered (currently starting at 2.1 cents per minute).

  Calls to a group of countries where Skype is most popular are available at a single SkypeOut Global Rate. Calls to countries covered under that rate include countries in North America, Europe, Australia, some countries in the Far East, and a few in South and Central America. Check the Skype website for exactly which countries are covered (www.skype.com/products/skypeout/rates).

- **SkypeIn**—To allow other people to call your Skype account on your computer, you can sign up for SkypeIn service. That service assigns a phone number to your Skype service so it can be reached from a traditional telephone.

  One advantage to this service is that you can have a phone number assigned from an area that is in a particular area from which you expect a lot of calls. In that way, people that call you from that same area can pay local charges, instead of long-distance charges. You, on the other hand, can be logged in from anywhere in the world that you can fire up your Skype account.

Some traditional extra telephone services are also available from Skype. For example, you can get Skype Voicemail (to answer your calls when you aren’t around) or Call Forwarding (to have your Skype calls forwarded to your traditional landline phone or mobile phone).

### Purchasing Accessories

Skype sells accessories that you can use with your Skype free and for-pay call services. The Skype Accessories Shop has the latest available products (http://accessories.skype.com). The following are some Skype products that might be useful to use with DSL.

- Headsets—Although you can purchase similar headsets to the ones that Skype offers at most stores that sell computer accessories, Skype offers some modestly priced headsets that include free SkypeOut minutes. Skype also sells a speaker/headset switch, to make it easier to change back to speakers when you are not making phone calls.

- Starter kit—If you are setting up several people at once to use Skype, a starter kit including a headset and software (usually Windows and/or Mac OS X) can help get everyone started. Some of the kits also include SkypeOut calling minutes.

If you get hooked on using Skype, but you prefer to use a handset to make and receive calls, Skype offers several different models of VoIP phones. Some of these phones connect to the computer via USB cables, whereas others connect wirelessly via a broadband Internet connection.

## RESTARTING DSL TO USE SKYPE

If you followed the procedure for installing Skype and the ALSA sound system, the extensions you need should already be set up to be loaded the next time you reboot DSL. If, when you boot DSL, you indicate that you want to use the ALSA sound system, you don’t even need to run any setup commands to start ALSA. It should just work.

Here’s an example of what you should enter at the boot prompt when you restart DSL to start the ALSA sound system (so you can use Skype):

```
boot: dsl alsa
```

If ALSA doesn’t start for some reason, try running the alsa_snddevices and alsa_init commands, as described in the “Setting Up ALSA Sound in DSL” section earlier in this chapter. You might also need to use other boot options if, for example, you had saved your MyDSL extension to some directory other than a top-level mydsl directory on a local hard disk or pen drive.

## TROUBLESHOOTING SKYPE

Skype requires an active Internet connection, working sound card, microphone, and speakers/headphones to be able to make audio calls. If any of those items isn’t working properly, you won’t be able to make audio calls with Skype.
