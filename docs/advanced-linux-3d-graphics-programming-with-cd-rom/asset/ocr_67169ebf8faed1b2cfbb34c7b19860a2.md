# # Lighting

Polygons, as we have treated them until now, have all been single-colored. We'll now look at some methods of combining color and light so that our polygons look more realistic.

For our purposes, we model light as a single, integer intensity value which changes the bright-ness of a particular color. Therefore, we combine light and color to arrive at a final lighted color. This is accomplished by means of lighting tables. In the lighting table, we simply look up the color along one axis, and the light intensity along the other axis, and find an entry in the table that tells us the final color with the specified intensity. For colors specified directly with red, green, and blue values (as opposed to through a palette), we split the lighting tables into three separate red, green, and blue tables, solely for the reason of saving memory.

![](bbox=[0.06, 0.37, 0.92, 0.88])

We define intensities as going from 0 to a certain predefined maximum integer light level, MAX_LIGHT_LEVELS. A light intensity of 0 combined with any color yields black; a light inten-sity of MAX_LIGHT_LEVELS combined with a color yields the original color at full intensity.