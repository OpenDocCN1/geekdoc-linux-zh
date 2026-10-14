
## Windows Compatible Enterprise Encryption Comes to Linux

## File Encryption Solution Framework for Linux

Maybe you’re wondering if you’re truly reading The NT Insider. Is this really an article on Linux? Well, yes and no. For years, we’ve been working on and writing about our on-access transparent File Encryption Solution Framework (FESF). This Solution Framework provides everything you need to build your own custom fast, reliable, file encryption product with no kernel-mode development required. We provide all the kernel-mode code, including an Isolation Minifilter and all the supporting code that performs the actual encryption using the Windows CNG system. Plus, we provide a complete user-mode reference implementation (written in C++) that you can use to start your project.

You define the policy that determines which files get encrypted or decrypted on access, based on the parameters you establish: The accessing application, the path or name of the file being accessed, the user or group doing the access, or just about any other factor you can envision.

We’ve had clients take FESF and go to market with their own complete, finished, product in less than six months. We think that’s pretty remarkable.

## Not Everybody Uses Windows!

Yup… it surprised us too. OK, it didn’t surprise everyone at OSR but, it surprised a lot of us. Well, maybe not really a lot of us, but… at least it surprised Peter. Anyhow, indeed not everyone on the planet uses Windows. There are actual people who run Linux on their servers and workstations. And, not surprisingly, these folks need on-access transparent file encryption.

While there are a couple of good quality transparent file encryption solutions for Linux already, none of them has anything near the flexibility that FESF provides. For example, they don’t allow you to specify that you only want to encrypt *.odt files in a given directory. Or that you only want those *.odt files transparently encrypted/decrypted when they’re opened with LibreOffice Writer (as opposed to say, when they’re accessed using catdoc).

And, of course, none of the existing Linux data encryption applications are compatible with FESF for Windows.

## Introducing: FESF for Linux

OSR’s File Encryption Solution Framework (FESF) for Linux provides you with the ability to create your own enterprise grade, highly flexible, transparent on-access file encryption/decryption solution on Linux. FESF for Linux comprises a native (kernel-mode) layered file system, written from the ground-up to support file access interception and file encryption activities. Using FESF for Windows as its inspiration, FESF for Linux allows your product to make its policy decisions in real-time from user-mode. Using FESF for Linux you can create a customized, powerful, and flexible transparent data encryption product with no kernel-mode programming. FESF for Linux comes with user-mode code that you can use as the basis for your product, giving you a head start on your development effort.

## Quick-Start Your Project: Transparent File Encryption

- OSR supplies all kernel-mode code
- You dynamically determine policy per file, on each access, entirely from user mode.
- Quality, commented, sample code supplied.
- High performance.

| Windows | Linux |
|---|---|
| Proven, in multiple commercial products. Available NOW. | Currently under development. Join our Early Adopter Program |
| sales@osr.com | |

## I Tried !Analyze-V...Now What?

You’ve seen our articles where we delve into analyses of various crash dumps or system hangs to determine root cause. Want to learn the tools and techniques yourself? Consider attendance at OSR’s Kernel Debugging & Crash Analysis seminar.

Amherst, NH (OSR) 4-8 December

## Peter Pontificates

## We Need a Driver Developer Conference!

![](img/feabf7ef0b3bb3419a0ef4d863642d48_3_0.png)

Back in 2015, I blogged and pontificated at great length about how I welcomed the improved openness and communication that seemed to be happening between Microsoft and the Windows driver development community. Of course, things could hardly have gotten worse than they were during the era that took us from Windows 7 to Windows 8. Oh, the stories I could tell. For example, I remember a major IHV (total sales in the realm of US$15 billion) that happened to be a client of ours being told that Microsoft wasn't interested in engaging with them, and if they wanted to know what was going on in Windows they could ask the OEMs to whom they sold their hardware.

Ouch! Things could only improve from there, right?

Well, they DID improve from there. Radically. And, thankfully, those days are long over. Still, even at the dawn of the new glasnost in 2015, I was calling for ever more and better two-way communications between Microsoft and us third party driver devs. And all the points I made in my December 2015 **Driver Pontification** calling for Even Better Communication still stand today.

Starting with Windows 8 and on through Windows 10, there have been tons of changes in the Windows ecosystem. There have been some key architectural changes to both the I/O and Power Management subsystems. We've witnessed the introduction of Windows RT, the introduction of Windows Mobile, the advent of Windows Phone, the introduction of Windows IoT Core (on x86 and ARM), support for the Raspberry Pi, support for the Snapdragon 835, introduction of OneCore, support for x86 emulation on ARM, and the introduction of Windows 10 S. And that's just to name a few of the most interesting things that have happened in the last couple of years.

Oh, I almost forgot to mention: In this same time period, the C/C++ compiler that's part of Visual Studio was largely re-written. And something called Universal Drivers was introduced (if you haven't grasped this, it's a biggie). And changes to INF files have been recommended. And who can miss the changes that have taken place to driver signing?

![](img/feabf7ef0b3bb3419a0ef4d863642d48_3_1.png)

What's notable to me is that *all the changes I mentioned, plus many others, significantly impact driver developers.*

What's even more notable is that there have been few opportunities for driver developers to come up to speed on these changes. It's definitely not like it was back in the bad old days. Most of the information on these topics is "out there" somewhere. Much has been documented on MSDN or on a blog. There are Channel 9 videos on several of these topics. Heck, we've written articles here in The NT Insider on a number of these topics as well.

But, by and large, driver devs have had to find their own way when it came to figuring out what's new for Windows driver developers. They've had to discover, search out, identify, and attempt to consume information about each topic. They read an article here, they watch a video there. And they've had little help piecing together the bigger picture.

CONTINUED ON PAGE 5
