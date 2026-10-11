
## Review Free software

### RTS GAME

#### 0 A.D. Alpha 21 Ulysses

From Carthaginians to Romans, rewrite ancient history

![](img/1f330653f83dcf0397f7d224ce8bbc16_89_0.png)

Above You start with an acropolis, and resources nearby, but will you emulate the success of ancient Athens?

- **Pros**
  - Good graphics, sound, and game progression. Online multiplayer options. Regular improvements and updates.
- **Cons**
  - A lot of yet-to-be-implemented features, so you may be playing Age of Empires for a little while yet.
- **Great for...**
  - Having fun while pretending to be learning history.
- [play0ad.com/](http://play0ad.com/)

If you ever doubt that the human race takes play seriously, take a look at the amount of hours that go into the **collaborative development** of open source games. Since the previously access-to-code-by-invitation game was relicensed under the GNU GPL in 2009 development has accelerated, and releases have been made regularly. O A.D. is still in alpha, but it's very playable, and well worth investing a little time in, whether you like RTSes, or are just interested in this historic period.

Unlike computing, calendars count from 1, and there was no year zero - hence the licence to adopt the name, and play a little fast and loose with history, where gameplay demands sacrifices in accuracy. The interface lets you get straight to playing, with sensible defaults already selected, so that there is no need to make decisions about things you don't yet understand.

The in-game manual will also help to keep you going as you marshal resources, and build alliances, to try and emerge victorious on the Attic plains. Players need to keep on top of military campaigns and defence, while building up enough resources to advance from village to town - and eventually city - unlocking technological advances along the way.

### INTERACTIVE DRAWING LIBRARY

#### Quil 2.5.0

Art from code, and it can run in your browser, too

Normally we have a screenshot for graphics apps that we review, but since Quil is a library for **interactive drawings and animations**, the page won't bring them to life as well as you visiting the project's homepage or, better yet, **running the software**. Why would you? Well, Quil mines Processing - an artist-friendly API - with Clojure, a language so hot that you're seriously running out of excuses not to at least give it a try. Real soon.

As with all things Clojure, Lein makes for the simplest of installs - Lein new quil my-sketch, then open the generated core.clj file up in your favourite Clojure friendly editor (Emacs or Lighttable), and evaluate the file. The website is full of examples, as well as links to tutorials, and a chance to try online. Speaking of online, Quil also works with **ClojureScript** (using Processing.js), so sketches can be run directly in your web browser.

If you know Processing, it's a little disconcerting to see it getting an attack of the parentheses to fit the Clojure world, but the examples are helpful here in getting you acclimatised - try Grey Crottes on Quil's GitHub page. Quil can be expanded with middleware, such as **Navigation 3D**, which allows shooter-like navigation through 3D spaces. Sketches can also be made into runnable jars, for carrying to anywhere runtime the JVM. Fun and useful, what more could you want?

- **Pros**
  - Update functions (and therefore animations) without restarting: make art from maths!
- **Cons**
  - It's not pure Processing, and Clojure is a big shock to newbie's (until they love it!)
- **Great for...**
  - Enter new presentations and pop-up web-sites.
- [quil.info/](http://quil.info/)

### HIDS

#### Samhain 4.2.0

Don’t rely on luck to protect your servers - install a host-based intrusion detection system

**Security** - you know you need it, but **something always gets in the way**. If you have one, two or a handful of VPSes, and perhaps an internet-facing server or two at home - don’t forget to count that Raspberry Pi project - you’ll have at least thought about security, probably even have a firewall, and maybe even do daily software updates, but you’ll have been far too busy to get serious about Intrusion Detection software. Well, stop procrastinating, postponing and procrastinating, and take a look at Samhain.

One of the best host-based intrusion detection systems (HIDS), Samhain sits stealthily on your system monitoring packets and detecting file modifications - as well as searching for rootkits and detecting rogue SUID executables. It can run as a standalone monitor on a single server, or monitor multiple hosts, logging centrally - with all logs sent signed and encrypted, naturally.

Packages are in most repositories, but distros may have compiled Samhain without a feature you need, so consider downloading the source; Samhain provides instructions for checking its integrity. Dependencies are minimal for reasons of security, but it makes for an easy compile. The real work starts when you open /etc/samhain in your favourite editor: time to read through the weighty manual. The terse man page is a useful guide to many parts of Samhain, including running in stealth mode, with config hidden by steganography.

- **Pros**
  - Powerful and flexible Intrusion Detection System; the only serious rival to OSSEC.
- **Cons**
  - To get the most from it you’ll have to spend a lot of time reading the comprehensive manual.
- **Great for...**
  - Stock monitoring on your servers and home working sites
- [ta-samhain.de/samhain/](http://ta-samhain.de/samhain/)

### TERMINAL CLIENT

#### iTerm 1.4.1

Manage all of your remote terminal sessions with iTerm

![](img/1f330653f83dcf0397f7d224ce8bbc16_90_0.png)

If you regularly shell into remote machines, but are not using a tool for transparent sessions across networks like MC or Emacs’ TRAMP mode, then you may be fed up of dealing with **remembering the log-in details, and the extra work involved in file transfers**. Enter iTerm, a terminal emulator based on VTE with plenty of features to make your life easier.

As well as the standard bells and whistles of tabbed sessions, working remotely (SSH, sftp, or even telnet) is facilitated by bookmarks, encrypted password saving (and authentication by key), and remote file and directory management: X11 forwarding can also be carried out over SSH sessions. There are some editing features, and plenty of configuration options such as customised mouse behaviour, for those with a particular way of working.

Additionally, users can send the same commands to clusters of remote servers or local desktop sessions - which is also an excellent way to step through parts of a shell script for careful testing of its effects on your servers. Very useful. Fairly regular releases, with attention to bug fixes as well as new features, means users can be confident that time invested in this app will not be squandered.

![](img/1f330653f83dcf0397f7d224ce8bbc16_90_1.png)

**Above** iTerm takes the pain out of remote working, giving you the best features of command line and GUI

- **Pros**
  - Combines a good basic terminal client with convenient, time-saving features for working across networks.
- **Cons**
  - It’ll never be as powerful as working across machines from Emacs, MC, etc - but does it need to be?
- **Great for...**
  - Anyone who wants to remote session: from VPS to Raspberry Pi
- iTerm.sf.net/

### Get your listing in our directory

To advertise here, contact Luke (luke.biddiscombe@imagin-publishing.co.uk | +44 (0)1202 586431)

**RECOMMENDED Hosting listings**

**Featured host:**
www.cyberhostpro.com
0845 527 9345

![](img/1f330653f83dcf0397f7d224ce8bbc16_91_0.png)

![](img/1f330653f83dcf0397f7d224ce8bbc16_91_1.png)

**About us**
Cyber Host Pro are committed to provide the best cloud server hosting in the UK; we are obsessed with automation and have been since our doors opened 15 years ago! We've grown year on year and love our solid growing customer base who trust us to keep their business’s cloud online!

If you’re looking for a hosting provider who will provide you with the quality you need to help your business grow then contact us to see how we can help you and your business! We’ve got a vast range of hosting solutions including reseller hosting and server products for all business sizes.

**What we offer**
- Cloud VPS Servers – scalable cloud servers with optional cPanel or Plesk control panel.
- Reseller Hosting – sell web and email hosting to your clients; both Windows and Linux hosting available.
- Dedicated Servers – having your own dedicated server will give you maximum performance; our UK servers typically include same-day activation.
- Website Hosting – all of our web hosting plans host on 2015/16 SSD Dell servers giving you the fastest hosting available!

**5 Tips from the pros**

1. **Optimise your website images**
   When uploading your website to the internet, make sure all of your images are optimised for website! Try using jpegmini.com software, or if using Wordpress install the EWWW Image Optimizer plugin.
2. **Host your website in the UK**
   Make sure your website is hosted in the UK, not just for legal reason! If your server is overseas you may be missing out on search engine rankings on google.co.uk – you can check where your site is on www.check-host.net.
3. **Do you make regular backups?**
   How would it affect your business if you lost your website today? It is important to always make your own backups; even if your host offers you a backup solution it’s important to take responsibility for your own data.
4. **Trying to rank on Google?**
   Google made some changes in 2015. If you’re struggling to rank on Google, make sure that your website is mobile-responsive! Plus, Google now prefers secure (https) websites! Contact your host to set up and force https on your website.
5. **Avoid cheap hosting**
   We’re sure you’ve seen those TV adverts for domain and hosting for £1! Think about the logic; for £1, how many clients will be jam-packed onto that server? Surely they would use cheap C20 drives rather than 2.1k+ enterprise SSDs! Try to remember that you do get what you pay for!

**Testimonials**

- **Chris Michael**
  “I’ve been using Cyber Host Pro to host various servers for the last 12 years. The customer support is excellent, they are very reliable and great value for money! I highly recommend them.”
- **Glen Wheeler**
  “I am a website developer, I signed up with Cyber Host Pro 12 years ago as a small reseller, 12 years later I have multiple dedicated and cloud servers with Cyber Host Pro, their technical support is excellent and I typically get 99.9-100% uptime each month”
- **Paul Cunningham**
  “Me and my business partner have previously had a reseller account with Cyber Host Pro for 5 years, we’ve now outgrown our reseller plan, Cyber Host Pro migrated us to our own cloud server without any downtime to our clients! The support provided to us is excellent, a typical ticket is replied to within 5-10 minutes!”
