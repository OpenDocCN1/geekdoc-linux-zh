
一旦你获得了一个高分（超过 2000 分就非常富足可观了）并熟悉了我们的简单实现，你通过跟随学习、探索代码以及阅读后续的简要说明将获得更多收获。对于那些想要创建自己的项目的人，创建一个新文件夹，并使用 IDE 或 Leafpad（或者可能是 Geany）保存你自己的 `.py` 文件。

![](img/c72194f2c3aec198936695a665a5167c_89_0.png)

我们尝试使用了 Pygame 的许多功能，它的设计是为了让创建游戏和交互式应用程序变得简单

# 使用 Python 编写一个《星际入侵者》克隆版

接第 89 页

```python
self.all_sprite_list = pygame.sprite.Group()
self.intro_screen = pygame.image.load(
'data/start_screen.jpg').convert()
self.background = pygame.image.load(
'data/Space-Background.jpg').convert()
pygame.display.set_caption("Space Invaders\n")
self.screen.blit(self.game_font.render(
"PRESS SPACE TO PLAY", 1, WHITE), (274, 191))
pygame.display.flip()
self.control()
pygame.mouse.set_visible(False)
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

```python
def control(self):
    for event in event.event():
        if event.type == pygame.QUIT:
            GameState.start_screen = False
            GameState.end = True
        if event.type == pygame.KEYDOWN:
            if event.key == pygame.K_ESCAPE:
                GameState.start_screen = False
                GameState.end = True
            if event.key == pygame.K_LEFT:
                GameState.vector = -1
            elif event.key == pygame.K_RIGHT:
                GameState.vector = 1
            if event.key == pygame.K_SPACE:
                GameState.start_screen = False
                self.lives = 1
                score = 0
```

```python
def splash_screen(self):
    while GameState.start_screen:
        self.kill_all()
        self.screen.blit(self.intro_font.render(
"INVADERS", 1, WHITE), (265, 120))
        self.screen.blit(self.game_font.render(
"PRESS SPACE TO START", 1, WHITE), (105, 355))
        pygame.display.flip()
```

```python
def make_player(self):
    player = Player()
    self.player_group.add(player)
    self.all_sprite_list.add(player)
```

```python
def refresh_screen(self):
    self.all_sprite_list.draw(self.screen)
    self.scores = []
    pygame.display.flip()
    self.screen.blit(self.game_font.render(
"SCORE: " + str(self.score), 1, WHITE), (0, 0))
    self.clock.tick(self.refresh_rate)
```

```python
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

```python
def make_bullet(self):
    if GameState.game_time - self.player.speed:
        bullet = Bullet(0, BLUE, BLUE)
        self.bullet_group.add(bullet)
        self.all_sprite_list.add(bullet)
        bullet.rect.x = self.player.rect.x + 28
        bullet.rect.y = self.player.rect.y
        self.game_time = GameState.game_time
```

```python
def make_missile(self):
    if GameState.game_time - self.player.speed:
        missile = Missile(0, RED, RED)
        self.missile_group.add(missile)
        self.all_sprite_list.add(missile)
        missile.rect.x = random.randint(0, BARRIER_WIDTH)
        missile.rect.y = 0
        self.game_time = GameState.game_time
```

接第 93 页

# 编写一个《太空入侵者》克隆版

## 使用 Python 创建

```
missile.vector = 1
missile.rect.x = shooter.x + 15
missile.rect.y = shooter.y + 40
missile.speed = 10
self.missile_group.add(missile)
self.all_sprites.add(missile)
```

```python
def make_barrier(self, columns, rows, spacer):
    for col in range(columns):
        for row in range(rows):
            barrier = Block(WHITE, BLOCK_SIZE)
            barrier.rect.x = col * (200 + spacer)
            barrier.rect.y = row * (50 + 10) + 0
```
