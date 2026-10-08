
# OpenSource

06 News | 12 Opinion | 94 Letters

## Netflix service will finally get native Linux support

No more hacks required for browser-based playback

Subscription-based video streaming service Netflix has confirmed that it is working on bringing its browser-based playback system to Linux desktops, and is working with Canonical to introduce support into the Ubuntu Linux distribution.

Netflix is an incredibly popular service originally launched in the US offering films on DVD via post. This was soon overtaken by a video streaming service, which was launched in the UK in 2012 and that now boasts more than 50 million subscribers in 40 countries.

Sadly for Linux users, the digital rights management (DRM) wrapper that protects the Netflix content has been unavailable on Linux, with the exception of support introduced into Google’s Chrome OS in 2011 – until now. Netflix has confirmed that an update to the Network Security Services library enables the Google Chrome Stable browser to play Netflix content officially on Ubuntu Linux for the first time in the company’s history.

Previously, Linux users with Netflix subscriptions have had to install beta packages and then modify their browser’s User-Agent string to enable playback. Paul Adolph, an engineer at Netflix, was the first to suggest this would change: “Netflix will play with Chrome Stable in [Ubuntu] 14.02 [sic] if NSS version 3.16.2 or greater is installed,” he explained in a post to the Ubuntu-Devel-Discuss mailing list.

Adolph went on to explain that if Canonical could roll out 3.16.12 or newer as standard to Ubuntu 14.04, as a replacement for the 3.15.x tree locked into the long-term support (LTS) release earlier this year, “Netflix would be able to make a change so users would no longer have to hack their User-Agent to play.” Canonical confirmed to the list that it would do precisely that, with engineer Marc Deslauriers stating that he was “planning on bumping NSS to 3.17 in the stable releases as a security update [anyway].” This has been carried out for Ubuntu 14.04 and 12.04 now, putting native Netflix support a mere apt-get update away for Canonical’s many LTS users.

> I can make a case here to lift the User-Agent filtering which will make Netflix HTML5 play in Chrome turnkey with no hacks required.

Adolph responded, referring to server-side filtering that enables playback only on a preset whitelist of User-Agent strings which does not yet include Chrome on Linux. At the time of writing, that change had yet to be made; users who want Netflix playback in Chrome on Ubuntu and who have received the updated NSS package are advised to modify their User-Agent string to match Chrome on Windows until the change is made.

Thus far, Netflix has not publicly reached out to any other Linux distributions to offer native playback support, nor indicated if it intends to formally support browsers other than Chrome on the platform.

![](img/c7d3278283754436651c50a2e9c72912_5_0.png)

Above: Netflix has worked with Canonical to bring native playback to Ubuntu for the first time.

![](img/c7d3278283754436651c50a2e9c72912_5_1.png)

Right: Using the latest Google Chrome browser, native HTML5 playback is supported on Ubuntu.

## Linux calendar

- **3rd – 5th November**
  - **Code Mesh 2014**
    - ILEC Conference Centre, London, UK
    - codemesh.io

Starting with a day of tutorials before the two-day conference, Code Mesh offers a look at technology and programming languages off the beaten path including Datomic, Neo4j, F# and Haskell.

- **17th – 21st November**
  - **SUSECon 2014**
    - Hyatt Regency Grand Cypress, USA
    - susecon.com

Designed for SUSE users and developers, confirmed speakers include SUSE president Nils Brauckmänner and vice-president Michael Miller along with Forrester Research analyst James Staten.

- **ApacheCon Europe**
  - Corinthia Hotel, Budapest, Hungary
  - events.linuxfoundation.org

Designed for developers and users who want to address open source 'the Apache way', sponsors of ApacheCon Europe include Citrix, the Apache Software Foundation and WanDisco.

- **19th – 21st November**
  - **CloudStack Collaboration Conference Europe**
    - Corinthia Hotel, Budapest, Hungary
    - events.linuxfoundation.org

Taking place alongside ApacheCon Europe, C3CEU concentrates on the OpenStack platform for the development and management of virtual machines as a Service (aaS).

### ARCHITECTURE

## Red Hat pushes 64-bit ARMv8 support

Has eyes on the low-power data centre market

Red Hat has confirmed that it is heavily backing the 64-bit ARMv8 instruction set architecture (ISA) from Cambridge-based ARM, promising "a seamless experience" for its users across all supported ISAs.

Although delayed, the ARMv8 ISA is turning heads in the industry thanks to its high performance per watt characteristics. Although unable to offer the same raw peak performance as 64-bit x86 chips from AMD and Intel, ARMv8 processors draw considerably less power, enabling for higher density in the data centre – perfect, its proponents claim, for cloud computing tasks.

Red Hat has confirmed the launch of what it describes as the ARM Partner Early Access Programme to speed up the adoption of ARMv8, which is not compatible with x86 and AMD64 ISAs. "Within the 64-bit ARM ecosystem, Red Hat is focused on creating a singular operating platform that relies on common standards to foster the development of new applications," the company claimed in a launch statement.

"The goal is to maintain expected enterprise-class attributes such as reliability, security, and performance for applications that are largely available today as open source projects."

Although Nvidia and Samsung have both backed away from plans to release server-centric ARMv8 processors, companies including AMD and AppliedMicro have products available in the market now.

![](img/c7d3278283754436651c50a2e9c72912_6_1.png)

### FREE SOFTWARE

## FSF & Debian partner on free hardware database

The Free Software Foundation and the Debian Project have joined forces to expand and enhance h-node, a database of hardware that can be used under Linux without any proprietary software or firmware.

"By collaborating with h-node, Debian for the first time has the opportunity to join efforts with other free software communities on the assembly of a database of hardware that doesn't require anything outside the Debian main archive to work," explained Lucas Nussbaum, Debian Project leader of the move which will see the FSF providing infrastructure and support.

Previously, Debian users were not permitted to contribute to the database due to the presence of non-free repositories.

The partnership will see h-node accepting contributions from Debian users providing they are using only the default free software repository for testing.

![](img/c7d3278283754436651c50a2e9c72912_6_2.png)

## Mozilla Labs shut down

> “I don’t believe Labs was effective,” says Ian Bicking

Mozilla Labs, a think-tank and software development group in the Mozilla Corporation, has been closed down with many of its alumni shifting to the Mozilla Foundation instead.

Used for research and development, Mozilla Labs was home to everything from the JavaScript-powered PDF.js in-browser PDF viewer to the Tornado web cross-platform media player. Some projects from the site, including the Open Badges Initiative and the aforementioned PDF.js, proved extremely successful; others less so.

This month, former Mozilla Labs staff member Ian Bicking posted to his blog confirming that the division had been formally closed, something that up to that point Mozilla had not announced itself.

“It’s a little hard to tell – I guess we didn’t actually shutter anything, and though it was announced internally it is entirely unclear externally,” he explained. “But Mozilla Labs is definitely shut down. I understand the reason for closing Mozilla Labs. I don’t believe Labs was effective [and] I was not effective in it,” Bicking adds, before clarifying that Mozilla Research, which focused more on foundational web technologies than on software development like its sister group did, is still very much active.

Mozilla has since confirmed the quiet closure of the division, stating that it was officially closed down in February this year with no public notification. Mozilla’s Andreas Gal told website i-programmer.info about the move: “We integrated Mozilla Labs staff more closely into product teams instead of maintaining Mozilla Labs as a separate team... This allows each team to better sponsor research and innovation for their products.”

At the time of writing, Mozilla had yet to modify the Labs website (https://mozillalabs.com/en-US) to indicate its closed status.

![](img/c7d3278283754436651c50a2e9c72912_7_0.png)

## NHS adopts open platform database

> Spine2 system goes live with Ubuntu core, replaces decade-old predecessor

The National Health Service (NHS) has sent its Spine2 patient record database and messaging system live, replacing its proprietary Oracle predecessor with a fully open-source software stack.

First announced in 2013, Spine2 uses a bevy of popular open-source packages to drive the giant database: Ubuntu with HA Proxy, nginx, Puppet, Mustache, Flask, Python, Redis, RabbitMQ and Tornado, along with Riak to ensure data persistence. The system scales across commodity servers using Intel Xeon processors in multiple data centres.

“We have harnessed the latest technology to rebuild the most important NHS electronic system, built over ten years ago and today relied upon by thousands of health staff and patients every single day,” boasted Health and Social Care Information Centre (HSIOC) chief executive Andy Williams of the project. “Of equal importance is [that] we have ensured value for money: by bringing the system in-house, the day-to-day running costs are set to fall substantially.”

“Rebuilding such a massive and integral system was a huge challenge, not least in ensuring more than 20,000 organisations and the many thousands of people who rely on the system were able to continue accessing the Spine during the transition with minimal disruption. I am delighted that the HSIOC, supported by the commitment of several other organisations, has achieved this.”

The Spine2 project was supported by commercial partners BUSS and Basho, and represents one of the largest UK government deployments of an open software stack to date. Additional new functionality is planned for the system over the next year and this includes an information sharing application focused on child protection.

![](img/c7d3278283754436651c50a2e9c72912_7_1.png)

8 www.linuxuser.co.uk
