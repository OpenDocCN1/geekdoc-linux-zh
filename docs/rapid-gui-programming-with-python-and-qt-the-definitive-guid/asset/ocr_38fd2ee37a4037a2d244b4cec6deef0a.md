```
```
def editMirrorHorizontal(self, on):
    if self.image.isNull():
        return
    self.image = self.image.mirrored(True, False)
    self.showImage()
    self.mirroredhorizontally = not self.mirroredhorizontally
    self.dirty = True
    self.updateStatus("Mirrored Horizontally" \
                      if on else "Unmirrored Horizontally")
```
```

This method is structurally the same as `editInsert()` and `editSwapRedAndBlue()`. The `QImage.mirrored()` method takes two Boolean flags, the first for horizontal mirroring and the second for vertical mirroring. In the Image Changer application, we have deliberately restricted what mirroring is allowed, so users can only have no mirroring, vertical mirroring, or horizontal mirroring, but not a combination of vertical and horizontal. We also keep an instance variable that keeps track of whether the image is horizontally mirrored.

The `editMirrorVertical()` method, not shown, is virtually identical.

```
```
def editUMirror(self, on):
    if self.image.isNull():
        return
    if self.mirroredhorizontally:
        self.editMirrorHorizontal(False)
    if self.mirroredvertically:
        self.editMirrorVertical(False)
```
```

This method switches off whichever mirroring is in force, or does nothing if the image is not mirrored. It does not set the dirty flag or update the status: It leaves that for `editMirrorHorizontal()` or `editMirrorVertical()`, if it calls either of them.

The application provides two means by which the user can change the zoom factor. They can interact with the zoom spinbox in the toolbar—its `valueChanged()` signal is connected to the `showImage()` slot that we will review shortly—or they can invoke the “edit zoom” action in the **Edit** menu. If they use the “edit zoom” action, the `editZoom()` method is called.

```
```
def editZoom(self):
    if self.image.isNull():
        return
    percent, ok = QInputDialog.getInteger(self,
                            "Image Changer – Zoom", "Percent:",
                            self.zoomSpinBox.value(), 1, 400)
    if ok:
        self.zoomSpinBox.setValue(percent)
```
```