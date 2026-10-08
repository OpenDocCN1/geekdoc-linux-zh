# # Program a Space Invaders clone with Python

Continued from page 89

```
self.all_sprite_list = pygame.sprite.Group()
self.intro_screen = pygame.image.load(
'data/start_screen.jpg').convert()
self.background = pygame.image.load(
'data/Space-Background.jpg').convert()
pygame.display.set_caption("Space Invaders\n
self.screen.blit(self.game_font.render(
"PRESS SPACE TO PLAY", 1, WHITE), (274, 191))
pygame.display.flip()
self.control()
npygame.mouse.set_visible(False)
Player.image = pygame.image.load(
'data/ship.png').convert()
Player.image.set_color(BLACK)
Alien.image = pygame.image.load(
'data/Alien.png').convert()
Alien.image.set_color(WHITE)
GameState.end = False
GameState.start_screen = True
GameState.vector = 0
```

```
def control(self):
    for event in event.event():
        if event.type == pygame.QUIT:
            GameState.start_screen = False
            GameState.end = True
        if event.type == pygame.KEYDOWN:
            if event.key == pygame.K_ESCAPE:
                GameState.start_screen = False
                GameState.end = True
                self.kill_all()
            if event.key == pygame.K_LEFT:
                GameState.vector = -1
            elif event.key == pygame.K_RIGHT:
                GameState.vector = 1
            if event.key == pygame.K_SPACE:
                GameState.vector = 0
                GameState.start_screen = False
                self.lives -= 1
                self.score = 0
                self.make_player()
                self.make_defenses()
                self.alien_wave()
```

```
def splash_screen(self):
    while GameState.start_screen:
        self.kill_all()
        self.screen.blit(self.intro_font.render(
"INVADERS", 1, WHITE), (265, 120))
        self.screen.blit(self.game_font.render(
"PRESS SPACE TO START", 1, WHITE), (105, 355))
```

```
def make_player(self):
    player = Player()
    self.player_group.add(player)
    self.all_sprite_list.add(player)
```

```
def refresh_screen(self):
    self.all_sprite_list.draw(self.screen)
    self.alien_scores = []
npygame.display.flip()
    self.screen.blit(self.game_font.render(
"SCORE: " + str(self.score), 1, WHITE), (0, 0))
    self.clock.tick(self.refresh_rate)
```

```
def alien_wave(self):
    self.screen.blit(self.game_font.render(
"LIVES: " + str(self.lives), 1, RED), (10, 355))
    for column in range(BARRIER_COLUMN):
        for row in range(ALIEN):
            alien = Alien()
            alien.rect.center = (column * (ALIEN_SIZE + ALIEN_SPACE), row * (ALIEN_SIZE + ALIEN_SPACE))
            self.rect_group.add(alien)
            self.alien_group.add(alien)
            self.all_sprite_list.add(alien)
            alien.speed = -speed
```

```
def make_bullet(self):
    if GameState.game_time - self.player.speed:
        bullet = Bullet(0, BLUE, BLUE)
        self.bullet_group.add(bullet)
        self.all_sprite_list.add(bullet)
        bullet.rect.x = self.player.rect.x + 28
        bullet.rect.y = self.player.rect.y
        self.bullet.time = GameState.game_time
        self.shoot_bullet = False
```

```
def make_missile(self):
    if len(self.alien_group):
        shooter = random.random()
        if shooter <= 0.05:
            alien = random.choice(self.alien_group)
            missile = Ammo(RED, MISSI_SIZE)
```

Continued on page 93