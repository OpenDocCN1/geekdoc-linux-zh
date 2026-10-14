# Making an Edna Music Server in DSL

Damn Small Linux is a very good base for creating an Edna Music Server. It is compact, yet it has everything needed to run a basic server and the tools in place to do remote streaming, while accessing files locally and over a network. This means that one may have access to one’s music shared over a local network even if the music files are stored elsewhere on the Internet. With DSL plus Edna, you have the power to get your music where you want without having to worry about storing local copies, which is a problem that occurs in many office situations. Let’s explore how this is done.

# ABOUT THE EDNA MUSIC SERVER

The Edna Music Server was written in the Python scripting language by Greg Stein. He calls it a quick hack, which is not a term that does it justice. Edna is an HTTP server that allows users to stream audio files, including MP3, Ogg Vorbis (.ogg), and other audio files. It is compatible with XMMS (included in DSL) and other popular MP3 players such as Winamp, Sonique, and FreeAmp.

Edna is constructed so that you can browse a music selection remotely. It uses a URL construct that allows you to link to a specific song. Edna also automatically makes a playlist for directory structures that can be played in sequence or a random shuffle.

Edna also dynamically builds pages according to the underlying directory structure of your music collection. Thus, categorizing is very simple and logical. You can organize your music by using the names of your directories and subdirectories as the categories and subcategories. Similarly, Edna servers offer .m3u playlists