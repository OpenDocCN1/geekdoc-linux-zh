
![](img/740bd926461af28ed755753238e647a2_89_0.png)

**Figure 2:** After some basic brightness, contrast, and saturation correction, the grass looks too intense, while the mountains are too pale. This can be fixed with the help of the L*a*b* curves.

The lower curves are a slightly more unusual. In the example, I will mainly be focusing on *CC* and *CL*. Select the *Parametric* or *Standard* curve type. In *CC*, four sliders appear under the parametric curve, dividing the colors into four groups. *Neutral* lets you further wash out or intensify near-white, gray, or black colors. In the case of the sample photo, this mainly means the clouds.

It won’t hurt to reduce the color here. Because I have globally intensified the colors with the saturation slider in the exposure module, they have acquired a slight color cast. Set the value to *-67*. The next slider lets you change matte colors, which is useful for the forest and mountains. Choose, say, 50 here. Finally, I’ll reduce the intensity of the pastel colors, which mainly means the grass (Figure 3).

In the next step, select the *Standard* curve type for *CL*. Click the top button in the vertical toolbar to the right of the curve diagram. When you move the mouse into the preview window, RawTherapee shows you – in the curve graphic – the area of the curve that holds the color you are currently pointing to. You can increase the intensity of dark colors by clicking a point near the bottom of the curve and dragging it upward. Initially, even light colors become more intense, because the upper half of the curve has automatically shifted upward. You can correct this by moving a point in the upper half slightly downward. The curve should now have an inverted S shape.

## Detailed Adjustments

Let’s highlight the structure of the clouds in *Local* (hand symbol). Enable the module in the titlebar and click *Add* in the *Settings* field. In the preview window, a red-bordered oval with a red circle in the center appears; move this to the cloud. In *Spot method* in the *Tools* panel, select *Full image*. After doing so, the application will only show you the circle. This selects all the colors in the image that are similar to the color below the image.

In *Add tool to current spot*, select the *Local Contrast* and *Wavelets* effect. Further down you will find the matching settings. Although they are similar to the local contrast settings in the *Details* tab, they also include a *Scope* slider. You can use it to control how similar the selected colors must be to those in the center of the selection. High values mean that RawTherapee also includes less-similar colors. This is why you only want to set this value to about 25; this applies the effect to the sky only. Then set the value for *Radius* to 100 and to 0.67 for the *Overall Strength*.

Now I’ll darken the blue mountains in the background a bit. To do this, create another selection as described above, but keep the *Normal* Spot mode. Move the center of the spot to a blue spot in the area of the mountains. Then enlarge the spot by dragging the four points on the oval outward across the entire mountain. Reduce the number of colors included using Range (Color Tools).

![](img/740bd926461af28ed755753238e647a2_89_1.png)

**Figure 3:** Use the *CC, LC,* and *CL* curves to independently manipulate saturation and brightness for saturated and matte, and pastel colors and shadows, depths, and highlights, respectively.

![](img/740bd926461af28ed755753238e647a2_90_0.png)

Figure 4: If you reduce the range of the selection with the Range slider, RawTherapee changes only the blue of the mountains, but not the clouds that are also selected.

For effects that do not come with their own range sliders, you can control the range with the global slider. These include color tools such as Color and Light. If you restrict the area, the application changes only the blue of the mountains and ignores the clouds, which are also selected (Figure 4). Add the Color and Light tool to this second selection and set the Brightness there to -5.

To finish up, there are only a few small tasks left to complete. Straighten the image, reduce the noise, and remove the car fragment on the right edge of the image using the spot removal tool. You will find the rotation tool in Transform | Lens Corrections. Basically, you will want to go for the Select Guideline function instead of setting the angle. In Select Guideline, trace a vertical or horizontal line in the preview. In the sample image, for example, the lamp is a good choice for this.

## Remove Distracting Objects

To remove distracting objects from an image, enable the spot removal tool in Details. As soon as you click on the pencil icon, the mouse cursor turns into a small cross, and you can set a point to remove the car fragment. Hold down Ctrl and click on the offending element. You will then see two small concentric circles at this point. Drag the inner circle outward to make it larger.

Actually, there are two brushes on top of each other now: The place covering the target area is at the bottom, and the one for the source area is at the top. Click on the circles and move the upper brush to the place you want to blend the car with – in this case, an area of the image to the left of the car (Figure 5). Except when removing very small spots, you will typically need to set several points to remove the object completely. Finally, use the pencil icon again to hide the brush marks or the retouched areas in the preview.

![](img/740bd926461af28ed755753238e647a2_90_1.png)

Figure 5: The new spot removal tool lets users remove distracting objects, provided they are not too large.

![](img/740bd926461af28ed755753238e647a2_91_0.png)

Figure 6: The new AMAZE+Bilinear demosaicing algorithm produces more granular noise, which the eye finds more pleasing.

Figure 7: Chromatic aberrations are frequently very stubborn; you may have to modify the automatic correction results manually.

## Minimize the Noise

Zoom into the image and check the image noise and sharpness in each image area by moving the view. To do this, first click on the magnifying glass on the right side of the toolbar. Although the landscape photo has seen some intensive touch-up work, the image noise is relatively low. But the image can still be optimized even further. Before you enable noise reduction, experiment a bit with Color Interpolation under Raw. This is mainly about the Method: Although AMAZe is the default value here, you should always try the AMAZe+Bilinear algorithm, too. RawTherapee divides the image into high and low texture areas using an edge detection filter. For zones that have a rich structure, it uses the sharper AMaZDeescreeining method, and for more monotonous areas, the softer Bilinear algorithm to nip any noise in the bud, so to speak. The AMaZDe+Bilinear method will not necessarily attenuate the noise. The results look finer grained and more pleasing to the human eye (Figure 6). If you still find this too intense, enable Noise Reduction under Details. This removes the color noise, which is fine for newer cameras up to about ISO 1600.

![](img/740bd926461af28ed755753238e647a2_91_1.png)

Don’t be too sensitive about image noise – this is a mistake most inexperienced photographers make. On the one hand, noise often doesn’t even matter with newer cameras. Even images up to ISO 6400 are basically no longer a problem today. And low noise is not one of the most important characteristics of good photos. In fact, a certain amount of noise often even looks aesthetically pleasing, or at least more natural than a smoothed-out photo. Don’t be afraid of high ISO values and don’t denoise too aggressively.

## Correcting Lens Aberrations

Correcting lens aberrations such as chromatic aberrations, vignetting, and distortion plays an important role in landscape photography. I will demonstrate this step with the help of two more sample photos, because there are virtually no errors of this type in the Mostviertel landscape.

Chromatic aberrations (a.k.a. purple fringing) are color fringes that often appear at contrasting edges, such as trees or branches in front of a bright sky. Automatic correction is already enabled in RawTherapee. However, sometimes the color fringes persist quite stubbornly, and you have to adjust the default configuration. You will find the settings for this in Raw in the last group Chromatic Aberrations of the first module Sensor with Bayer Matrix.

Zoom into the image and move the view to the image area where the chromatic aberrations occur (Figure 7). Uncheck the Auto-correction box and then change the positions of the sliders for Red and Blue below it. Which slider you need to move in which direction depends on the color of the aberration. Blue and violet color fringes are very common.

For blue chromatic aberrations, move the Blue slider to the right until the color fringe disappears. If you see a yellow or yellow-green color fringe near the removed blue color fringe, you have adjusted the slider too far. For violet aberrations, you also need to move the Red slider a little to the right. Finally, check all image areas in the 100-per- cent view. What often happens, when chromatic aberrations are removed, is that new ones are created in other areas.

![](img/740bd926461af28ed755753238e647a2_92_0.png)

Distortion happens all the time. Pinchushion distortion often occurs, especially with wide-angle lenses, and can be quite annoying for images with trees or a straight horizon. You will find the settings for this in Transform at the bottom of the Lens Corrections module. The Automatic option is selected in the Lens Correction Profile group. But this will not work with many cameras because lens selection fails. You need to select the right lens in the list next to Lens. After that, both the distortion and the vignetting should disappear.

What happens if you can’t find the correction profile for your lens in the Lensfun database? In this case, first try the automatic distortion

Figure 8: In most cases, distortion and vignetting can be corrected using the Lensfun lens-correction profiles.
