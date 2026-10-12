The last method we must consider is the timeout() method that is called every INTERVAL milliseconds by the timer. We will look at the method in two parts, since there are two aspects to what it does.

```
```
def timeout(self):
    if not Running:
        return
    angle = self.angle
    while True:
        angle += random.randint(-9, 9)
        offset += random.randint(3, 15)
        x = self.x() + (offset * math.sin(math.radians(angle)))
        y = self.y() + (offset * math.cos(math.radians(angle)))
        if 0 <= x <= SCENESIZE and 0 <= y <= SCENESIZE:
            break
    self.angle = angle
    self.rotate(random.randint(-5, 5))
    self.setPos(QPoint(x, y))
```
```

If the global Running Boolean is False, we do nothing and return. Otherwise, we calculate a new position for the head based on a small random change to its angle of direction (±9°), and a small movement (3–15 logical units). To avoid the multipede wandering out of the scene, we keep moving and turning it until its new (x, y) position is within the scene’s boundaries.

Once we have the new coordinates, we record the angle that was used, rotate the head slightly, and set the head’s position. At this point, collisions may have occurred as a result of the movement.

```
```
for item in self.scene().collidingItems(self):
    if isinstance(item, Head):
        self.color.setRed(min(255, self.color.red() + 1))
    else:
        item.color.setBlue(min(255, item.color.blue() + 1))
```
```

We ask the scene for all the items that the head has collided with. If it has hit another head, we make this head a bit redder, and if it has hit a segment, we make the segment it has hit a bit bluer. If a head’s red color component reaches 255, the head (and therefore the entire multipede, including all the segments) will be removed from the scene. The removals take place in the form’s timer event, as we saw earlier (page 372).

Now we will look at the Segment implementation. Its initializer is a bit longer than the Head’s initializer, but the boundingRect(), shape(), and paint() methods are much simpler as a result.

```
```
class Segment(QGraphicsItem):
    def __init__(self, color, offset, parent):
```
```