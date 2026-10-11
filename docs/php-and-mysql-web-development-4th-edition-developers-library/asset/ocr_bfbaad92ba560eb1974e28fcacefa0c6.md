**Unimplemented function.** The OpenGIS specification also defines the following `LINESTRING` property function, but MySQL does not implement it: `ISRING()` .

The following functions take a spatial `MULTILINESTRING` value `mIs` in internal format and return a property of the value.

+   - `GLENGTH(mIs)`
+     - Returns the length of `mIs` as a double-precision value. The length of a `MULTILINESTRING` value is the sum of its constituent `LINESTRING` values.
+   - `ISCLOSED(mIs)`
+     - Returns 1 if `Is` is closed, 0 if it is not, and −1 if it is `NULL`. A closed `MULTILINESTRING` is one for which the starting point and end point are the same for each of its constituent `LINESTRING` values.

The following functions take a spatial `POLYGON` value `poly` in internal format and return a property of the value.

+   - `AREA(poly)`
+     - Returns the area of `poly` as a double-precision number.
+   - `EXTERIORRING(poly)`
+     - Returns the exterior ring of `poly` as a `LINESTRING` value.
+   - `INTERIORRING(poly,n)`
+     - Returns the *n*-th interior ring of `poly` as a `LINESTRING` value. Rings are numbered beginning with 1.
+   - `NUMINTERIORRINGS(poly)`
+     - Returns the number of interior rings in `poly`.

The following function takes a spatial `MULTIPOLYGON` value `mpoly` in internal format and returns a property of the value.

+   - `AREA(mpoly)`
+     - Returns the area of `mpoly` as a double-precision number.

**Unimplemented functions.** The OpenGIS specification also defines the following `MULTIPOLYGON` property functions, but MySQL does not implement them: `CENTROID()` , `POINTONSURFACE()` .

The following functions take a spatial `GEOMETRYCOLLECTION` value `gc` in internal format and return a property of the value.

+   - `GEOMETRYN(gc,n)`
+     - Returns the *n*-th geometry of `gc`. The type of the return value depends on what the *n*-th geometry is. Geometries are numbered beginning with 1.
+   - `NUMGEOMETRIES(gc)`
+     - Returns the number of geometries in `gc`.