# # Chapter 10

```
{
    case 'image/jpeg':
        $this->gdbResource = imagecreatefromjpeg($file);
        break;
    case 'image/png':
        $this->gdbResource = imagecreatefrompng($file);
        break;
    case 'image/gif':
        $this->gdbResource = imagecreatefromgif($file);
        break;
}
// Retain the alpha information
imagesavealpha($this->gdbResource, true);
// Save the file to the local filesystem
public function save($file)
{
    switch ($this->type)
    {
        case 'image/jpeg':
            imagejpeg($this->gdbResource, $file);
            break;
        case 'image/png':
            imagepng($this->gdbResource, $file);
            break;
        case 'image/gif':
            // Convert back to palette
            if (imageistruecolor($this->gdbResource))
            {
                imagergptocolorpalette($this->gdbResource, false, 256);
            }
            imagegif($this->gdbResource, $file);
            break;
    }
}
// Display the image in the browser
public function display()
{
    switch ($this->type)
    {
        case 'image/jpeg':
            header("Content-type: image/jpeg");
            imagejpeg($this->gdbResource);
            break;
        case 'image/png':
            header("Content-type: image/png");
            imagepng($this->gdbResource);
            break;
        case 'image/gif':
            // Convert back to palette
            if (imageistruecolor($this->gdbResource))
```