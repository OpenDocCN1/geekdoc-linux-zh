# WINDOWS SPECIALITIES

If a .pc file is found in a directory that matches the usual conventions (i.e., ends with `lib\pkgconfig` or `share\pkgconfig`), the *prefix* for that package is assud to be the grandparent of the directory where the file was found, and the *prefix* variable is overriden for that file accordingly.

If the value of a variable in a .pc file begins with the original, non-overriden, value of the *prefix* variable, then the overriden value of *prefix* is used instead.