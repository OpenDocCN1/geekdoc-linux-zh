# # X Logical Font Descriptions

In X, a font's name contains 14 (I) parts. The 14 parts are listed in Table 4.2.

**TABLE 4.2 Fields in an X Logical Font Description**

| Field | Meaning |
| :--- | :--- |
| Foundry | The organization that created the font. Examples are adobe and bitstream. |
| Family | The general font family, such as courier or times. |
| Weight | The weight of the font. Examples are bold or medium. |
| Slant | The slant of the font. Examples are i for italic, o for oblique, and r for upright. |
| Set Width | The “compactness” of the font. It is usually normal but may be condensed or semicondensed. |
| Additional Style | Additional style parameters. This is hardly ever used. The only example I could find was a Lucida font that specified sans in this field. |
| Pixel Size | Specifies the size of the font in pixels. |
| Point Size | Specifies the size of the font in tenths of a point. You should usually specify point size and not pixel size; the X server will calculate the correct pixel size to use. |
| X Resolution | The horizontal resolution of the font in dots per inch. Used only for bitmap fonts. |
| Y Resolution | The vertical resolution of the font in dots per inch. Used only for bitmap fonts. |
| Spacing | The spacing scheme used by the font. Can be p for proportional, m for monospaced, or c for constant spacing. |
| Average Width | The average width (in tenths of a pixel) of all characters in the font. |
| Registry | The authority responsible for determining the encoding scheme of the font. For example, all fonts encoded according to the ISO 8859 standard have a registry of iso8859. |
| Encoding | The particular encoding scheme. Western European characters are encoded using the iso8859·1 scheme, whereas Hebrew characters are encoded using iso8859·8. |