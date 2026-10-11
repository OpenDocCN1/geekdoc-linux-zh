
## Programming Snapshot – Go Geolocation Game

Collections, but can only sort points with X/Y coordinates. Line 41 creates a lookup hash map. It maps the longitude and latitude of the photos to the JPEG images on the disk. When the algorithm comes back with the coordinates of a desired image later on, the program can find, load, and display the associated image.

### Controlled Randomness

From the representatives of all the chosen clusters, the Schmitz game initially needs to select a secret target picture for the player to guess. It then opens the game with a random starting image, but it would not be a good idea to pick the secret image, even by accident! The Go `math/rand` standard solution in Go delivers randomly and equally distributed index positions between 0 (inclusive) and `len()` (exclusive), thus picking purely random elements from the array.

The `randPickedExcept()` function starting in line 75 of Listing 2 now picks a random element from the array passed into it, without ever revealing the element that resides in the `exclIdx` place. This is accomplished by the algorithm only selecting the elements in index positions 1...`N` from the elements in the index range 0...`N`, neglecting the first image in the list. And, if the choice happens to fall on the forbidden `exclIdx` position, the function simply delivers the θ item, which was previously excluded from the pick, as a replacement. This way, all photos, except the secret one, have an equal probability of being picked as a starting point.

### Slimming Down

Listing 3 helps to load the scaled down cell phone photos into the GUI. One difficulty here is that many cell phones have the bad habit of storing image pixels in a rotated orientation when taken and noting in the header that the image needs to be rotated either 90 or 180 degrees for display purposes [7].

This display behavior is handled by the imageorient package that Listing 3 pulls in from GitHub in line 5, auto-rotating each image before it is handed to the GUI for display. Also, nobody really wants to move massive photos around on the screen. Instead, the `nfmt/resize` package (also from GitHub) creates handy thumbnails from the large photos with the help of the `Thumbnail()` function in line 26.

Listing 4 computes the distance between the photo shoot locations of two image files and the angle from 0 to 360 degrees at which you would have to start walking to get from A to B. As the earth isn't a flat surface, calculating these numbers isn't as easy as on a two-dimensional map, but the formulas dealing with the required 3D geometry are not too complicated and already available online [8]. In line 8, the `hike()` function takes the longitude (`lng*`) and latitude (`lat*`) from the GPS data of two photos and taps into the functions of the `golang-geo` library, including `GreatCircleDistance()` and `BearingTo()` to determine the distance and bearing to travel from one photo to the other.

To convert the route's bearing, available as a floating-point number ranging from 0 to 360 degrees into a compass direction such as north or northeast, line 16 divides the angle by 45, rounds the result to the nearest integer, and then accesses the array slice in line 15 with that index. Index 0 is for north, 1 is NE for northeast, and so on. If the index drops below 0, which can happen with negative angles, line 19 simply adds the length of the array slice to arrive at an index that addresses the array slice from the end instead.

```go
// Listing 3: image.go
package main

import (
	"fmt/io/fyne/v2/canvas"
	"github.com/disintegration/imageorient"
	"github.com/nfmt/resize"
	"image"
	"os"
)

const DspWidth = 300
const DspHeight = 150

func dispDim(w, h int) (dw, dh int) {
	if w > h {
		// landscape
		return DspWidth, DspHeight
	}
	// portrait
	return DspHeight, DspWidth
}

func scaleImage(img image.Image) image.Image {
	dw, dh := dispDim(img.Bounds().Max.X,
		img.Bounds().Max.Y)
	return resize.Thumbnail(uint(dw),
		uint(dh), img, resize.Lanczos3)
}

func showImage(img canvas.Image, path string) {
	nimg := loadlImage(path)
	img.Image = nimg.Image

	img.FillMode = canvas.ImageFillOriginal
	img.Refresh()
}

func loadlImage(path string) *canvas.Image {
	f, err := os.Open(path)
	panicOnErr(err)
	defer f.Close()
	raw, _, err := imageorient.Decode(f)
	panicOnErr(err)

	img := canvas.NewImageFromResource(nil)
	img.Image = scaleImage(raw)

	return img
}
```

```go
// Listing 4: gps.go
package main

import (
	geo "github.com/kellyjxn/golang-geo"
	"math"
)

func hike(lat1, lng1, lat2, lng2 float64) (float64,
	string, error) {
	p1 := geo.NewPoint(lat1, lng1)
	p2 := geo.NewPoint(lat2, lng2)

	bearing := p1.BearingTo(p2)
	dist := p1.GreatCircleDistance(p2)

	names := []string{"N", "NE", "E", "SE", "S", "SW",
		"W", "NW", "N"}
	idx := int(math.Round(bearing / 45.0))

	if idx < 0 {
		idx = idx + len(names)
	}

	return dist, names[idx], nil
}
```

### Widget with Something Special on Top

We hope to cover every single special case conjured up by creative software engineers. For example, in the Schmitz game, the guesser clicks on a photo in the right pane, to have the game move it to the left. Photos don't normally take clicks, but button widgets do. And they, in turn, define callbacks to perform the intended action in case of an event.

The schmitzle GUI application relies on the Fyne framework to whip up a native-looking graphical application on the desktop with plain vanilla Go code. Previous articles in this column [9] have plumbed the depths of this excellent tool [10] many a time. Fyne comes with a whole range of label, listbox, button, and other widgets out of the box, but it can't.

With just a little code, you can quickly program extensions in Fyne to add the desired, albeit nonstandard, behavior. Listing 5 defines a new widget type named `clickImage` starting in line 13. It is composed from a canvas object with a thumbnail image and takes a callback that it invokes when the user clicks on the photo with the mouse.

Thanks to Go's built-in inheritance mechanism for structures, `widget.BaseWidget` on line 14 derives the structure from Fyne's base widget, thus providing it with the display, shrink, or hide functions common to all widgets. In addition, the add-on widget needs to call the `ExtendBaseWidget()` function in the constructor.

```go
// Listing 5: gui.go
package main

import (
	"fyne.io/fyne/v2"
	"fyne.io/fyne/v2/canvas"
	"fyne.io/fyne/v2/container"
	"fyne.io/fyne/v2/widget"
	"math/rand"
	"os"
	"time"
)

type clickImage struct {
	widget.BaseWidget
	image *canvas.Image
	cb    func()
}

func NewClickImage(img *canvas.Image, cb func()) *clickImage {
	ci := &clickImage{}
	ci.ExtendBaseWidget(ci)
	ci.image = img
	ci.cb = cb
	return ci
}

func (t *clickImage) CreateRenderer() fyne.WidgetRenderer {
	return widget.NewSimpleRenderer(t.image)
}

func (t *clickImage) Tapped(_ *fyne.PointEvent) {
	t.cb()
}

func makeUi(w fyne.Window, p fyne.Preferences) {
	rand.Seed(time.Now().UnixNano())

	var leftCard *widget.Card
	var rightCard *widget.Card

	quit := widget.NewButton("Quit", func() {
		os.Exit(0)
	})

	var restart *widget.Button

	reload := func() {
		leftCard, rightCard = makeGame(p)
		vbox := container.NewVBox(
			container.NewGridWithColumns(2, quit, restart),
			container.NewGridWithColumns(2, leftCard, rightCard),
		)
		w.SetContent(vbox)
		canvas.Refresh(vbox)
	}

	restart = widget.NewButton("New Game", func() {
		reload()
	})

	reload()
}
```
