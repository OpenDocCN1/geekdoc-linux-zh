
![](img/740bd926461af28ed755753238e647a2_16_0.png)

How often you record is closely related to episode duration. It’s far better to produce two 30-minute podcasts than a single podcast lasting an hour. Generally, the more frequently you can produce a podcast the better. Once a week is ideal. This keeps your podcast in the minds of your listeners and helps them to remember you. Once every two weeks is another good option, especially to start with, but once a month might be too little. Either way, the more frequent your podcasts, the larger your monthly download figures will be, and this helps hugely if you ever want to sell advertising sponsorship.

It’s essential you communicate clearly when a podcast episode is expected – and stick to it. Rain or shine, PulseAudio failure or hard drive crash. It’s the one thing that differentiates amateurs from the professionals; professionals understand that listeners need an absolutely predictable routine. Predictable releases are a sign of strength and stability, because no one wants to invest time in something that may ultimately peter out, and the more your listeners need to do to work out which was your last episode and which is your next, the fewer listeners you’ll have.

## People Power

Three or four co-hosts is an ideal number because it allows listeners to get to know your personalities, and it allows them to feel they’re among friends (Figure 1). Co-hosts can help share the burden of being engaged, doing the research, playing devil’s advocate, and approaching a discussion from another perspective, or by simply compensating for another host who can’t make it. It helps if you already know each other and are already comfortable and relatively unguarded in each other’s company. Even for well-planned or scripted podcasts, it’s the unpredictable parts that listeners enjoy, and spontaneous, divergent conversations are an important part of this. It’s important that differing opinions on topics are reflected by the hosts. A podcast should not become a vanity project for the strongest personality, or worse, the person who puts the podcast together.

The role of the main host is the most important and under-appreciated in the whole podcast enterprise. The main host is the person asking questions on behalf of the listener, sensitive to whether what’s being talked about is likely to be understood. This is important whenever you have experts talking – an expert might assume a level of knowledge that you can’t also assume of your listenerhip, and it’s the main host’s job to ask for clarification on points or challenge an assumption when needed. The main host should also try to make sure all hosts are equally included in the conversation, perhaps by asking a quieter host their opinions, or breaking into the monologue of a verbose participant to give someone else a chance to share an opinion.

Whoever drives the podcast needs to be subtle and transparent. If they’re doing a brilliant job, no one will know. This is a thankless task that might even weaken your position within the hosting dynamic as you play more than one role from more than a single angle, but it’s essential that someone adopts this persona, and it might as well be the podcast founder.

![](img/740bd926461af28ed755753238e647a2_16_1.png)

**Figure 1:** The rapport between co-hosts is sometimes more important than the podcast idea itself, although mixing up personalities and opinions is also vital.

![](img/740bd926461af28ed755753238e647a2_17_0.png)

**Figure 2:** Performing and recording a podcast live can be a lot of fun, but it doesn’t necessarily result in the best quality episodes.

## Publishing and Analytics

With a plan agreed, recordings made, and the important step of editing complete (Figure 2), you’re ready to share your podcast with the world. We’d obviously recommend releasing your podcast under a Creative Common license, and many Linux-based podcasts choose either the Creative Commons Attribution-NonCommercial (CC BY-NC) or the Attribution-ShareAlike (CC BY-SA) licenses. The CC BY-SA license is ideal if you’re not concerned about people deriving monetary value from your work. Choosing either will also help with music and logo choices, because you’re then free to use similarly licensed creative works within your own podcast.

Using music in the intro, the outro, and segment transitions adds a professional production quality to your podcast. Although music and design work can be commissioned cheaply through platforms such as Fiverr, choosing from Creative Commons-licensed media gives you much greater control. Many Creative Commons music tracks, for instance, are provided as a pack of *stems*, bundling the individual tracks used to produce the final mix. This gives podcasters a lot of flexibility, letting them repeat a section of the music, remove vocal tracks, or create an entirely different mix suitable for embedding within the podcast.

The next big question is how you intend to host your podcast. A 30-minute mono podcast is usually about 30MB. A moderately successful podcast might have 10,000 listeners, and this requires around 300GB of bandwidth per episode. Self-hosting is usually good enough to start with, especially if you can grab a domain name related to your podcast, and you can either set up a dynamic CMS such as WordPress for posting content related to each episode, or you can use a static site generator updated for each release. Another important aspect is community feedback, and it’s worth offering several options, including email or web-based comments, alongside cheaper and easier-to-maintain options like an IRC presence, a Telegram group, or a Discord server. Spotify will do all this for you, but you lose control over how you might publish or aggregate your podcast later.

Of course, a podcast wouldn’t be a podcast without an RSS feed. RSS remains central to how you publish your podcast and how people listen to it. An RSS file is an XML-formatted text file that podcast players parse to understand where the podcast is located and which episodes are available (see the box entitled “Podcast RSS Format”).

RSS is simple enough to create manually, and you’ll find plugins for WordPress and other sites that can make the process even more painless. It is also easy to get your podcast included in Apple’s Podcasters Program [2], Spotify’s equivalent [3], or YouTube, although you’ll need to agree and accept certain content, RSS-formatting, and encoding requirements for Apple and Spotify. You can bypass all of this using a podcast aggregating service or host, who will happily serve your podcasts, submit them for inclusion on the most popular services, and even negotiate advertising on your behalf. Aggregating services usually cost very little up front, although they will take a substantial cut from any advertising revenue.

On the subject of money, making any from a podcast is difficult and shouldn’t be your principal motivation. You might, however, make enough money to help with hosting bills and equipment. For open source and Linux-related podcasts, you might want to consider using Patreon [4], which enables listeners to make a small contribution to the running of the podcast. You can encourage this with additional content for backers, early access to episodes, or access to a podcast feed without any advertising. You can also sell merchandise (Figure 3) or sell advertising for the podcast. Selling advertising is a unique skill, but if you're up for the challenge, nothing is stopping you from getting in touch with companies you think might be interested to negotiate advertising, sponsorship, or product reviews. These are usually negotiated in advance per quarter or per six months, depending on a company's advertising budget, and advertisers will want to see consistent listener numbers, listening hour numbers, and a certain level of engagement with their adverts – either through affiliate links or through podcast-specific coupon codes or similar.

![](img/740bd926461af28ed755753238e647a2_17_1.png)

**Figure 3:** One way to help fund a podcast is through merchandise, which can often be made and dispatched on demand, with the supplier taking a certain percentage of the overall price.

## Podcast RSS Format

The RSS file includes links to each episode, metadata such as duration and size, and a section that links back to your general web presence (Figure 4). Listeners subscribe via the RSS URL and are pushed to new episodes as soon as they're released. The easiest way to create your own RSS feed is to either use a plugin for your CMS, such as WordPress, or to copy one for a similar podcast. It can help to find an XML editor, such as Red Hat's XML extension for Visual Studio Code, and use it to remove all but one podcast episode, then simply replace the metadata with your own. The podcast-specific content is held with the `<channel>` elements, with the first section used to describe the global data for your podcast, such as its name, a description, and links to images and logos. Beneath this, each episode is encapsulated within `<item>` tags that contain similar details specific to each episode.

Providing meaningful statistics is surprisingly difficult and quite different from the web-based metrics you might be familiar with. Many podcast players will open multiple streams for a single listener, cache podcasts offline, or never make it through a single episode. You can carefully craft analytics for unique IP addresses and megabytes downloaded, but it's usually easier to rely on the far more advanced tools provided by Apple Podcasts, Spotify, and YouTube, which can usually highlight the most popular sections and also help promote engagement through reviews or comments. These numbers can then be extrapolated to include self-hosted downloads. But try not to think about the numbers too much. They can be a useful metric for growth, but they naturally fluctuate throughout the year, and it is often difficult to derive meaningful data from them. Stay true to your original plan and vision, but most importantly, have fun. Everything else will look after itself.

### Info
- 1. History of English Podcast: [https://historyofenglishpodcast.com](https://historyofenglishpodcast.com)
- 2. Apple Podcasts for Creators: [https://podcaster.apple.com/](https://podcaster.apple.com/)
- 3. Spotify for Podcasters: [https://podcaster.spotify.com](https://podcaster.spotify.com)
- 4. Patreon: [https://www.patreon.com](https://www.patreon.com)

### Author
Graham Morrison is a distinguished Linux author and editor. He writes the FOSSPicks column for *Linux Magazine* and has been podcasting nearly every two weeks (and now every week) for 14 years, first on *TuxRadar*, which he edited, produced, and published, and more recently on *Late Night Linux*.

![](img/740bd926461af28ed755753238e647a2_18_0.png)

```xml
<?xml version="1.0" encoding="UTF-8"?>
<rss version="2.0"
  xmlns:content="http://purl.org/rss/1.0/modules/content/"
  xmlns:atom="http://www.w3.org/2005/Atom"
  xmlns:dc="http://purl.org/dc/elements/1.1/"
  xmlns:podcast="https://podcastindex.org/ns/1.0"
  xmlns:itunes="http://www.itunes.com/dtds/podcast-1.0.dtd"
  xmlns:rns:googleplay="http://www.google.com/schemas/rns/play"...>
<channel>
  <title>Linux Magazine</title>
  <link>https://www.linux-magazine.com/feed/</link>
  <description>Linux Magazine is a podcast that takes a look at what's happening in the Linux world.</description>
  <lastBuildDate>Wed, 29 Jun 2023 14:56:38 +0000</lastBuildDate>
  <language>en-US</language>
  <sy:updatePeriod>daily</sy:updatePeriod>
  <sy:updateFrequency>1</sy:updateFrequency>
  <generator>https://wordpress.org/?v=6.2.2</generator>
  <image>
    <url>https://www.linux-magazine.com/wp-content/uploads/2016/12/cropped-favicon-32x32.png</url>
    <title>Linux Magazine</title>
    <link>https://www.linux-magazine.com</link>
    <width>32</width>
    <height>32</height>
  </image>
  <atom:link href="http://pubsubhubbub.appspot.com/" .../>...
</channel>
```

Figure 4: The XML used within a podcast RSS feed is easy to understand, but using an XML-aware editor, such as Visual Studio Code, will help you catch any errors that might creep in.
