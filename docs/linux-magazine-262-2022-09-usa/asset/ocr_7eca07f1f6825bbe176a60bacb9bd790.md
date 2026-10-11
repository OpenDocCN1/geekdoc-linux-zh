# IN-DEPTH

# Programming Snapshot – Go Geolocation Game

```
Listing 4: gps.go

01  package main
02
03  import (
04      geo "github.com/kellyjxuann/goiand-geo"
05      "math"
06  )
07
08  func hike(lat1, lng1, lat2, lng2 float64) (float64,
          string, error) {
09      p1 := geo.NewPoint(lat1, lng1)
10      p2 := geo.NewPoint(lat2, lng2)
11
12      bearing := p1.BearingTo(p2)
13      dist := p1.GreatCircleDistance(p2)
14
15      names := []string{"N", "NE", "E", "SE", "S", "SW",
          "W", "NW", "N"}
16      idx := int(math.Round(bearing / 45.0))
17
18      if idx < 0 {
19          idx = idx + len(names)
20      }
21
22      return dist, names[idx], nil
23  }
```

length of the array slice to arrive at an index that addresses the array slice from the end instead.

hope to cover every single special case conjsured up by creative software engineers. For example, in the Schmitz game, the guesser clicks on a photo in the right pane, to have the game move it to the left. Photos don't normally take clicks, but button widgets do. And they, in turn, define callbacks to perform the intended action in case of an alert.

# Widget with Something Special on Top

The schmitzle GUI application relies on the Fyne framework to whip up a native-looking graphical application on the desktop with plain vanilla Go code. Previous articles in this column [9] have plumbed the depths of this excellent tool [10] many a time. Fyne comes with a whole range of label, listbox, button, and other widgets out of the box, but it can't

With just a little code, you can quickly program extensions in Fyne to add the desired, albeit nonstandard, behavior. Listing 5 defines a new widget type named clickImage() starting in line 13. It is composed from a canvas object with a thumbnail image and takes a callback that it invokes when the user clicks on the photo with the mouse.

Thanks to Go's built-in inheritance mechanism for structures, widget.BaseWidget on line 14 derives the structure from Fyne's base widget, thus providing it with the display, shrink, or hide functions common to all widgets. In addition, the add-on widget needs to call the ExtendBaseWidget() function in the

```
Listing 5: gui.go

01  package main
02
03  import (
04      "fyne.io/fyne/v2"
05      "fyne.io/fyne/v2/canvas"
06      "fyne.io/fyne/v2/container"
07      "fyne.io/fyne/v2/widget"
08      "math/rand"
09      "os"
10      "time"
11  )
12
13  type clickImage struct {
14      widget.BaseWidget
15      image *canvas.Image
16      cb func()
17  }
18
19  func NewClickImage(img *canvas.Image, cb func())
          *clickImage {
20      ci := &clickImage{
21          ci.ExtendBaseWidget(ci)
22          ci.image = img
23          ci.cb = cb
24          return ci
25      }
26
27  func (t *clickImage) CreateRenderer() fyne.WidgetRenderer {
28      return widget.NewSimpleRenderer(t.image)
29  }
30
31  func (t *clickImage) Tapped(_ *fyne.PointEvent) {
32      t.cb()
33  }
34
35  func makeUi(w fyne.Window, p fyne.Preferences) {
36      rand.Seed(time.Now().UnixNano())
37
38      var leftCard *widget.Card
39      var rightCard *widget.Card
40
41      quit := widget.NewButton("Quit", func() {
42          os.Exit(0)
43      })
44
45      var restart *widget.Button
46
47      reload := func() {
48          leftCard, rightCard = makeGame(p)
49          vbox := container.NewVBox(
50              container.NewGridWithColumns(2, quit, restart),
51              container.NewGridWithColumns(2, leftCard, rightCard),
52          )
53          w.SetContent(vbox)
54          canvas.Refresh(vbox)
55      }
56
57      restart = widget.NewButton("New Game", func() {
58          reload()
59      })
60
61      reload()
62  }
```