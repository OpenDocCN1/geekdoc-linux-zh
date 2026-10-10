
## TUTORIALS  Photo restoration

![](img/5cfcf2f4448dccdd1c5c2a2851544557_69_0.png)

Credit: www.gimp.org

### Capture and restore old photos and slides

**Mike Bedford** shows you how to scan, repair and archive old film-based photos, to give your family heirlooms a new lease of life.

![](img/5cfcf2f4448dccdd1c5c2a2851544557_69_1.png)

**OUR EXPERT**
Mike Bedford
has an extensive collection of film-based photos, both his own and those he’s taken quite an interest in preservation and restoration.

- **QUICK TIP**
- Be sure to clean as much loose dust, dirt and hairs off your photos before you scan them. Don’t use a cloth, though, because that could cause scratches, and don’t try using a solvent unless you know exactly what you’re doing. Instead, use a compressed air can, but don’t hold it too close because that could damaging your photo by freezing it.

**T**raditional photos, by which we mean the prints, negatives or slides produced by the chemical processes that predated digital photography by well over 100 years, can be remarkably resilient. In fact, it’s been suggested that, while we might have inherited photos taken by our grandparents or great grandparents, it’s much less likely that today’s digital photos will be available to future generations.

Our reference to resilience requires some clarification, because it’s by no means guaranteed. For a start, while black-and-white photos are based on a chemical reaction involving silver halides, which are moderately fade-resistant, the dyes used in colour photography were not nearly as forgiving. And second, even in the realm of black-and-white photography, the resilience assumes that the prints or negatives have been well looked after. In reality, this might not be the case. Prints have often been well handled over the decades, so creases, tears, fingerprints and tea stains will have taken their toll. And while negatives are probably not been handled as much, in poor storage conditions – at a non-ideal temperature or high humidity – they could have become dirty, damaged by water or infested by mildew, to name just a few risks.

All this sounds rather depressing, because those old photos might be the only records you have of long- gone family members. However, there is a solution. Here we’re going to see how to restore photos that have lost their former glory by using photo-editing software. In fact, you might just be able to make them better than Great Uncle George would have remembered them.

### Digitisation

Because your old photos only become eligible for editing once they’re in the digital domain, we first need to give some thought to digitisation. If the media is a slide, three probably won’t be an associated print, so you’ll need to scan the slide, and this involves much the same processes as for scanning negatives.

To take an extreme example, the old disk film that was introduced by Kodak in 1982 had a negative measuring just 8x10mm (0.3x0.4 inches), which is very significantly smaller than a typical 4x6-inch print. The relevance of this difference depends on your scanner’s resolution. However, if we assume 1,200x1,200dpi, that would result in a difference between 360x480 pixels (less than 0.2MP) for the digitised negative and 4,800x 7,200 pixels (35MP) for the digitised print. With the former being totally inadequate, the recommendation would be to scan the print, even though you wouldn’t be achieving the quality that the 35MP figure might suggest, because the optical resolution inherent in the print would probably be lower. Be sure to save your scan in a lossless format such as TIFF and, during the editing process, save all the intermediate results in the same lossless format, so that compression artefacts don’t build up. If necessary, though, you can also save a copy of the final results as a JPEG. Also, in the case of a black-and-white photo, save the scan as a monochrome file – grayscale – since it’ll give you better results and a smaller file size than if you saved it as a colour file.

![](img/5cfcf2f4448dccdd1c5c2a2851544557_69_2.png)

> If you have a collection of old photos, their condition might leave something to be desired. However, all is not lost.

Another scanning option to bear in mind, especially if you decide that your scanner isn’t up to scratch, is to use the services of a professional scanning company. Obviously, this will cost a reasonable amount per scan but, depending on how many photos you want scanning, it could be cheaper overall than investing in a new scanner. However, since your prints or negatives will probably be irreplaceable, don't ignore the risk, however small, that's posed by sending them to the scanning company. Using a signed-for postal service offers greater security; better still, use a local company so you can deliver and collect your photos by hand.

![](img/5cfcf2f4448dccdd1c5c2a2851544557_70_0.png)

### Photo editing

Here we're going to be looking at several steps of photo editing, using GIMP, but we should point out at the start that you won't always have to carry out all the steps. Each step addresses a particular defect in your old photo, and which of them you need to carry out depends on which of the defects are present. As another word of introduction, you're probably going to be spending quite some time in restoring each of your photos, so be sure to save differently named versions after each step so, if one step goes wrong, you can return to the result of the previous step.

If you have scanned a negative, the first job is to convert it to a positive. Proper transparency scanners can usually convert the image to a positive automatically, but if you use our alternative methods, as described in the boxout (over the page), you have to do it manually. In the case of a black-and-white negative, this is easy to do in GIMP - just select Colour > Invert. With a colour negative, though, while this is still the first step, the invert function isn't enough, as you'll see when you try it.

You'll notice that the resultant inverted image has a strong cyan colour cast, because physical colour negatives have a red cast. As a next step, therefore, you need to remove the colour cast. So, select the Colour Picker tool and click into the border of the film - the area behind the image - and this assigns the colour of the border as the foreground colour. Now, select Layer > New Layer and, in the dialog box, select Foreground Colour against Fill With before clicking on OK. Assuming the Layers dialog is displayed, you'll see the new layer above the one with the image. Make sure this new layer is selected and choose Subtract against Mode. The colour of the border is subtracted from all the colours in your image, and this makes it look a lot closer to what you've been expecting. It's probably still not perfect, though, so you need to do some editing, using the usual methods of colour correction - Colour > Auto > White Balance would be a good one to try at first, and might be sufficient. If not, read on for our discussion of restoring colour photos that have become discoloured.

We're now going to look at the various steps involved in the restoration process - the first few apply to either black-and-white or colour photos, and the final one to colour only. If your photo has suffered physical damage, the worst affected parts are usually the corners and the edges. In that case, you need to crop it to remove any areas that are either totally missing or so badly damaged that they can't be repaired. In the case of damage like tears, the inner parts of which could be more easily repairable than the outer parts, it may be necessary to select a cropped area, which is something of a compromise. In deciding the extent of the cropping, we suggest you crop as little as necessary, without considering the aspect ratio. After all, if you subsequently want to reproduce it with a conventional aspect ratio, it is an easy job to crop it further. To crop, select Tools > Selection > Rectangle Select and then draw a rectangle around the part of the image you wish to keep. In the case of dog-eared or torn prints, a degree of cropping is your first task.

![](img/5cfcf2f4448dccdd1c5c2a2851544557_70_1.png)

### PROTECT THE SOURCE MATERIAL

Having digitised and subsequently restored your family heirlooms, you probably won't want to abandon the source material. After all, a 100-year-old family album has a unique appeal and sentimental value, even if the photos it contains aren't as good as your edited digital equivalents. What's more, you might feel that slides, negatives and photos have historical interest, and that it would be a shame to totally lose an appreciation of old-school photography. Unfortunately, however, those old photos will continue to degrade, and it's inevitable that, sooner or later, they will be of no value whatsoever. There is some good news, though, namely that with proper care, you can slow down their deterioration.

That care all comes down to storage, so use appropriate containers. Ordinary paper contains acid, so store paper or photographic prints in envelopes, folders and/or boxes that are acid-free and intended for storing valuable and old documents. Make sure the folders or envelopes are a suitable size for their contents, as documents that are free to move excessively may get damaged. Ideally, make sure prints and negatives are separated using sheets of acid-free paper, so they don't stick together. And store the boxes or envelopes vertically, using acid-free padding to prevent the

![](img/5cfcf2f4448dccdd1c5c2a2851544557_70_2.png)

documents from slumping if any boxes aren't full. Suitable document archiving boxes are available from www. preservationequipment.com. Using proper containers will keep your photos dark, which is good, but also store them in a medium-low humidity, moderately low temperature environment.
