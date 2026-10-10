Like formatted and unformatted memos, Delphi provides a data-aware version of an image: **TDBImage**. **TDBImage** is lacking, however, because it only correctly stores and retrieves bitmaps (*.BMP files). A robust application should store bitmaps, JPGs, and (almost) any other image type that the user might want to store.

There are at least three methods that you can use to store multiple image types in a dataset. They include:

+   * Creating a separate field that will be used to store the image type. Use this field value to determine how to store/load the image.
+   * Writing a value to the BLOB field indicating the image type, immediately followed by the image data.
+   * Using a third-party imaging library to do the work for you.

The following sections discuss these options.

# Using a Separate Field to Store the Image Type

One way to track the type of image stored in a dataset is to add a separate field, perhaps named `ImageType`, to track the type of image. Say, for the sake of argument, that your application can store BMPs and JPGs. You would set up constants for each image type, like this:

```
const
IMAGE_NONE = 0;
IMAGE_BMP = 1;
IMAGE_JPG = 2;
```

Presumably, the `ImageType` field contains the value `IMAGE_NONE` when the BLOB field is **NULL**. To implement this method correctly, you must remember to set the `ImageType` field whenever the user loads an image, and then reset it to `IMAGE_NONE` if the user clears the image.

# Streaming the Image Type as Part of the BLOB Field

With a little extra code, you can dispense with the additional field and store the image type in the BLOB field along with the image itself. Figure 4.2 shows conceptually what is involved with this method.

The following pseudo-code shows how you might implement this method:

```
procedure SaveImage;
begin
OpenOutputStream;
WriteImageType;
WriteImageData;
end;
```