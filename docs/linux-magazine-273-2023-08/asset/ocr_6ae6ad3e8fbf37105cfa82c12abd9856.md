# # TUTORIAL – RAWTHERAPEE WORKSHOP

![](bbox=[0.14, 0.1, 0.97, 0.44])

sharper AMaZDeescreeining method, and for more monotonous areas, the softer Bilinear algorithm to nip any noise in the bud, so to speak. The AMaZDe+Bilinear method will not necessarily attenuate the noise. The results look finer grained and more pleasing to the human eye (Figure 6). If you still find this too intense, enable Noise Reduction under Details. This removes the color noise, which is fine for newer cameras up to about ISO 1600.

Don’t be too sensitive about image noise – this is a mistake most inexperienced photographers make. On the one hand, noise often doesn’t even matter with newer cameras. Even images up to ISO 6400 are basically no longer a problem today. And low noise is not one of the most important characteristics of good photos. In fact, a certain amount of noise often even looks aesthetically pleasing, or at least more natural than a smoothed-out photo. Don’t be afraid of high ISO values and don’t denoise too aggressively.

# ## Correcting Lens Aberrations

Correcting lens aberrations such as chromatic aberrations, vignetting, and distortion plays an important role in landscape photography. I will demonstrate this step with the help of two more sample photos, because there are virtually no errors of this type in the Mostviertel landscape.

Chromatic aberrations (a.k.a. purple fringing) are color fringes that often appear at contrasting edges, such as trees or branches in front of a bright sky. Automatic correction is already enabled in RawTherapee. However, sometimes the color fringes persist quite stubbornly, and you have to adjust the default configuration. You will find the settings for this in Raw in the last group Chromatic Aberrations of the first module Sensor with Bayer Matrix.

Zoom into the image and move the view to the image area where the chromatic aberrations occur (Figure 7). Uncheck the Auto-correction box and then change the positions of the sliders for Red and Blue below it. Which slider you need to move in which direction depends on the color of the aberration. Blue and violet color fringes are very common.

For blue chromatic aberrations, move the Blue slider to the right until the color fringe disappears. If you see a yellow or yellow-green color fringe near the removed blue color fringe, you have adjusted the slider too far. For violet aberrations, you also need to move the Red slider a little to the right. Finally, check all image areas in the 100-per- cent view. What often happens, when chromatic aberrations are removed, is that new ones are created in other areas.

Distortion happens all the time. Pinchushion distortion often occurs, especially with wide-angle lenses, and can be quite annoying for images with trees or a straight horizon. You will find the settings for this in Transform at the bottom of the Lens Corrections module. The Automatic option is selected in the Lens Correction Profile group. But this will not work with many cameras because lens selection fails. You need to select the right lens in the list next to Lens. After that, both the distortion and the vignetting should disappear.

What happens if you can’t find the correction profile for your lens in the Lensfun database? In this case, first try the automatic distortion

Figure 8: In most cases, distortion and vignetting can be corrected using the Lensfun lens-correction profiles.