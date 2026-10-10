# > ## DESCRIPTION

**fc-cache** scans the font directories on the system and builds font information cache files for applications using fontconfig for their font handling.

If directory arguments are not given, **fc-cache** uses each directory in the current font configuration. Each directory is scanned for font files readable by FreeType. A cache is created which contains properties of each font and the associated filename. This cache is used to speed up application startup when using the fontconfig library.

Note that **fc-cache** must be executed once per architecture to generate font information customized for that architecture.