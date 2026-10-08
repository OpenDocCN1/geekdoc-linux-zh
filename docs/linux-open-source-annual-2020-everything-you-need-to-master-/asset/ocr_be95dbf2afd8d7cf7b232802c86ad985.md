Do more

# # Metadata management

Former NSA and CIA director Gen. Michael Hayden once said “We kill people based on metadata”. So let’s think about how to reduce yours.

When you take a photo (or movie), together with the picture data your camera stores a whole bunch of extra info called Exif (Exchangeable Image File) metadata. This includes stuff like the picture orientation, exposure time and focal length. It also includes information about the camera model, the time and, if the photographic device has a GPS unit (like a smartphone camera), the GPS coordinates too. Some devices even store their serial numbers, much to the chagrin of one movie pirate.

So you really ought to be careful about what you do with your photos, since this metadata betrays where and when you were. Obviously this isn’t a concern if you’re sharing photos with trusted viewers, since you’d probably tell them that anyway, but it’s not the kind of information you want to be sharing with strangers on the internet.

And it’s certainly not the kind of information you want to be sharing with giant companies that have access to huge amounts of other data about you that can be mined, cross-referenced and used to target advertising at you. When you upload a photo to Facebook, Instagram or anything of that ilk, that metadata is all erased (and your photo likely horribly resized and compressed) before the image is reproduced anywhere. But there’s no reason to suspect that the metadata doesn’t lie on in a database somewhere, ready to be digested by nebulous algorithms.

You can view Exif data in lots of ways; the website [https://exifinfo.org](https://exifinfo.org) enables you to upload files and view metadata. But uploading photos to random websites is probably not the type of thing you should endorse in a privacy feature. If you open your image in *GIMP*, then go to Image > Metadata > View Metadata, you’ll see the type of things that we’re on about. Besides Exif, you’ll see there are tabs for XMP and IPTC metadata (which are usually used to store names of people and places in the picture, as well as copyright information). GIMP’s Edit Metadata option only allows you to change XMP/IPTC information, but there are other ways to delete Exif data. The most direct is with the `Exiv2` tool, which we can install with:

```
`$ sudo apt install exiv2`
```

*Exiv2* can manipulate Exif data in all kinds of ways, but what we’re interested in is purging it altogether – and that’s easy. Suppose you have some photos in the current directory and you want to strip them of Exif data. First make sure that is really what you want to do – that data is useful for cataloging or post-processing purposes. It’s just not what you want to be giving to giant internet companies. If in doubt, copy the images to another directory (this is also a good place to resize them so they are treated more justly at the other side) and work on them there. Exif data is removed thusly:

```
`$ exiv2 rm *.jpg`
```

Tails includes *MAT* (the Metadata Anonymisation Toolkit) that can deal with not only Exif data, but metadata from documents, spreadsheets, torrents and audio files. Again, this data is useful – truly there is nothing more infuriating than an untagged MP3 file – but can also (at least partially) identify you. You may have set up *LibreOffice* with your name in the author field; you may be the only person using a particular version of an MP3 encoder specified in an ID3 tag; your machine’s hostname may have worked its way into a torrent file you created. Basically, if you want to share files and don’t want them to be traced back to you, you need MAT in your workflow.

# ## Vexacious indices

Windows 95 introduced the Recent Documents menu in its Start menu and ever since then desktop environments have become even more sophisticated about indexing the files you open. This is certainly handy – especially if you store everything on the desktop, you madman – but on a shared machine it’s something of a privacy risk.

If that machine gets stolen, or someone has access to your account, they can easily find the local files you’ve been working on, no matter how bad your filing system is. Gnome’s Tracker and KDE’s Baloo can both index the contents of documents as well as their metadata, so you can find them just by hammering a few keywords into the search screen. Very handy, but also very telling. Both of these can be tamed. Tracker can be disabled on an application-level basis, or you can tell it not to search particular locations – by default it indexes everything in your home folder. Baloo by default indexes all local, non-removable storage (and actually has its

Control Gnome’s Tracker daemon from this dialogue in the Settings panel, to prevent overzealous and possibly incriminating indexing.

![](bbox=[0.06, 0.71, 0.54, 0.95])