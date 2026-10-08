# Harden your browsers

The web browser might well be the most used application on your machine, so it deserves special attention.

W e've usually been pretty impartial about which browser you should use, but we're going to deviate from that slightly, at least for this feature. Chrome's always been a slick browser, but all that Googleyness baked in makes us queasy. Chromium is a better option, being entirely open source, devoid of Flash and generally less dependent on Google services. It's also easier to install than Chrome on most distros because of the rules about the latter's redistribution.

However, a change crept into both Chrome and Chromium last year that made us both wary. That changed concerned the 'Sign in to Chrome' functionality, which connects the browser to your Google account and can optionally sync bookmarks, extensions and browsing history – just like in Chrome

# OTHER BROWSERS

There are other browser options. The privacy-centric Brave browser (https://brave.com) is based on Chromium and has an interesting funding model. Users are rewarded BAT (Basic Attention Token) for viewing ads. BAT is based on the Ethereum blockchain, and tokens can be bought for cash, or showered upon your favourite YouTube stars. We're not really down with adverts, but if their revenue is used to develop better browsers, we might make an exception.

There's also the Ungoogled-Chromium project (https://github.com/Eelston/Ungoogled-chromium), which strives to be free of any and all Google web service dependencies, as well as enabling some enhanced privacy controls. In so doing, it challenges the notion that Chromium is pretty much Ungoogled Chrome. There are other, similar projects, most notably Iridium (https://iridiumbrowser.de) and Inox, which is a modular patchset to the Chromium codebase (https://github.com/gcajar/inox-patchset). Gnome and KDE both have their own browser projects, respectively Web (formerly Epiphany) and Falkon (formerly Quetzal), which are both much more lightweight than the usual suspects. Neither has any interest in harvesting your data.

![](bbox=[0.09, 0.76, 0.53, 0.95])

OS. Up until Chrome 69, this option was distinct from signing into Google services via their web pages – and this, we thought, was a good thing. But now, just signing into those services connects the whole browser with that account. We don't have a problem with signing into Google or indeed any other browser-wide service, but that should be done explicitly by the user.

We should point out that these enforced sign-ins don't currently sync bookmarks and so on. Google's privacy policy (see www.google.com/chrome/privacy/#browser-modes) just mentions that in the Signed in mode, the browser can connect to the user's Google Payments account – it doesn't imply that any additional data is sent to Google. However, we're cynical and even though no data is overtly shared now, such a change could easily creep in. So as such we're recommending Firefox, but that's just us. Obviously if you don't use your Google Account regularly (a good thing) none of that really matters. Read more about it on crypto guru Matthew Green's blog at http://bit.ly/1xf253crypto¹

Whichever browser you use, we'd recommend using an ad-blocker like uBlock Origin – though we're still in the publishing business, just so we'd also ask you to disable it for trusted, quality sites (that's a short list – Ed). There's too much dodgy business that goes on with third-party advertising networks; see, for example, our malware feature in LXF51. For related reasons we'd also recommend enabling the Do Not Track option in your browser's settings. By design this has to be set by the user – it's a signal that you send to advertisers to let them know you're not interested.

Browser extensions in general should be treated with caution, but we approve wholeheartedly of the EFF's HTTPSEverywhere, which ensures HTTPS is used wherever possible. Many sites often still accidentally link to HTTP resources, even if your connection to the main page is done over HTTPS. The EFF's Privacy Badger is a good shout too: instead of using pre-assigned blocklists Privacy Badger learns as it goes, so you might need to give it a few hits early on. Privacy

![](bbox=[0.55, 0.78, 0.92, 0.92])

Sometimes it's nice to know your unique in the world, but as far as web browsers go we want to be indistinguishable from the masses.