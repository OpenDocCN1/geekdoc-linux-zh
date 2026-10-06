# Part II: Using Fedora RHEL

+   - Unauthorized copying of copyright-protected material is never legal. Even legal video decodes do not make legal to copy commercial movies and other protected content and distribute them to others. There are questions as to whether or not, for example, it is legal to make a backup copy of a DVD (a commonly accepted legal practice with computer software). Any redistribution of movie, music, or other media content is not legal without the owner's permission.

Because patenting eliminates secret protection for the subject matter disclosed in the patent (or published patent application), many people have raised the question of why someone can't freely libdvdness (based on DeCSS decryption) to play DVD movies. Without copyright or patent coverage on CSS, it should not be illegal to distribute libdvdness and there's nobody to pay a license fee for using it. In the Digital Millennium Copyright Act (DMCA), DMCA might make DeCSS illegal because the technology is used to break an encryption scheme to circumvent copyrighted material.

As for the software matter, those have fought on several fronts relating to multimedia content. As noted earlier, the contention between many open source proponents is that software should be copyrighted and not patented (see the section "Understanding Multimedia and Legal Issues in Linux" earlier in this chapter).

With all that, the next parts of this chapter go on to describe which players are available to play a wide range of video content in Linux. It is up to you to work out the maze of codecs are free for you to use and in what ways.

# Understanding video content types

Before launching into the video players themselves, I want to try to clear up bit of confusion relating to video files and formats:

+   - Video file formats — A video file essentially describes the structure of a video file for combining audio and video content. That structure can also define things as subtitles and how audio and video are synchronized. However, a variety of video and audio codecs may have been used to encode content. So, just because you can play a video file that is marked as MPEG (.mpg), Audio Video Interleaved (.avi), QuickTime (.mov), RealMedia (.rm), Windows media (.wmv), Advanced Streaming Format (.asf), or other file, doesn't mean you can play all video files marked as.

+   - Video and audio codecs — Codecs are used to encode and decode video and audio content. A video encoded entirely with free software might use Theta to encode the video and Ogg Vorbis to encode the audio. Popular video codecs include MPEG-4, DivX, Xvid, RealVideo, and MJPEG.

Not all video codecs and file formats are suitable for streaming video. For example, AVI and MPEG-2 are not streamable. However, RealMedia, MPEG-4, and ASF format can be streamed, which reduces the load on a server and means you do not have to download an entire