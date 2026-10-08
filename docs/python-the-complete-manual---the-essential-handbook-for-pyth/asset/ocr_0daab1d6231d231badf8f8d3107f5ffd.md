# Create with Python

# Pivaders part 2: graphics and sound

# Loading the sprite sheet

07 Since we are inheriting from the Sprite class to create our Player class, we can easily alter how the player looks by changing pygame. First, we need to load our sprite sheet with pygame.image.load(). Since we made it with a transparent background, we can convert_alpha() to the end of the line so the frames appear correctly (without any background). We then use subsurface to set the PlayerImage to the middle sprite of the sheet, which has an initial size of 5. Changing this will alter the image drawn to the screen: '0' would draw it leaning fully left; '1' to the right.

```
GameState.end_game = False
GameState.start_screen = True
GameState.vector = 0
GameState.shoot_bullet = False
```

```
def control(self):
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            GameState.start_screen = False
            GameState.end_game = True
        if event.type == pygame.KEYDOWN \
            and event.key == pygame.ESCAPE:
                if GameState.start_screen:
                    GameState.end_game = True
                    self.kill_all()
        if GameState.start_screen:
            keys = pygame.key.get_pressed()
            if keys[pygame.K_LEFT]:
                GameState.vector = -1
                self.animate_left = True
                self.animate_right = False
            elif keys[pygame.K_RIGHT]:
                GameState.vector = 1
                self.animate_right = True
                self.animate_left = False
```

# Animation graphs

08 Slightly further down the list in the initializing code for our Game class, we also set two flags for our player: animate_left and animate_right. As you will see in the Control method of our Game class, we use these flags to when we want animations to happen with True and False. It also allows us to automatically animate the sprite back to its natural resting state (otherwise the ship will continue as if it's flying left when it has stopped).

```
GameState.vector = 0
self.animate_right = False
self.animate_left = False
```

```
if keys[pygame.K_SPACE]:
    if GameState.start_screen:
        GameState.start_screen = False
        self.lives = 2
        self.make_player()
        self.make_defenses(2)
        self.make_alien_wave()
```

```
GameState.shoot_bullet = True
self.bullet_fx.play()
```

# The animation method

09 We use flags in the code for the player: animate_player(). Here we use nested statements to control the animation and physically set the player image. It states that if the animate_right is True and if the current position is not what we want, we increment the ani_pos variable and set the player image. The Else statement then animates the sprite back to its resting state and the same logic is then applied in the opposite direction.

```
def animate_player(self):
    if animate_right:
        if self.ani_pos < 6:
            Player.image = self.sprite_sheet.subsurface(self.ani_pos*64, 0, 64, 61)
            self.ani_pos += 1
    else:
        if self.ani_pos > 5:
            self.ani_pos -= 1
            Player.image = self.sprite_sheet.subsurface(self.ani_pos*64, 0, 64, 61)
    if animate_left:
        if self.ani_pos > 0:
            self.ani_pos -= 1
```

![](bbox=[0.396, 0.915, 0.875, 0.945])