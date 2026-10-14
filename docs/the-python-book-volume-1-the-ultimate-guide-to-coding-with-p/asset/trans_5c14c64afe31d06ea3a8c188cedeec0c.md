

# 使用 Python 创建

```python
#!/usr/bin/env python3

import pygame, random

BLACK = (0, 0, 0)
BLUE = (0, 25, 255)
WHITE = (255, 255, 255)
RED = (255, 0, 0)
ALIEN_SIZE = (30, 40)
ALIEN_SPACER = 20
BARRIER_ROW = 10
BARRIER_COLUMN = 4
BULLET_SIZE = (5, 10)
MISSILE_SIZE = (5, 5)
BLOCK_SIZE = (10, 10)
RES = (800, 600)

class Player(pygame.sprite.Sprite):
    def __init__(self):
        pygame.sprite.Sprite.__init__(self)
        self.image = pygame.Surface(BULLET_SIZE)
        self.rect = self.image.get_rect()
        self.rect.x = RES[0] / 2 - self.size[0] / 2
        self.rect.y = 520
        self.travel = 7
        self.speed = 350
        self.time = pygame.time.get_ticks()

    def update(self):
        self.rect.x += GameState.vector * self.travel
        if self.rect.x < 0:
            self.rect.x = 0
        elif self.rect.x > RES[0] - self.size[0]:
            self.rect.x = RES[0] - self.size[0]

class Alien(pygame.sprite.Sprite):
    def __init__(self):
        pygame.sprite.Sprite.__init__(self)
        self.image = pygame.Surface(ALIEN_SIZE)
        self.rect = self.image.get_rect()
        self.has_moved = 0
        self.vector = [1, 1]
        self.travel = [ALIEN_SIZE[0] - 7, ALIEN_SPACER]
        self.speed = 700
        self.time = pygame.time.get_ticks()

    def update(self):
        if GameState.alien_time - self.time > self.speed:
            if self.has_moved[0] < 12:
                self.rect.x += self.vector[0] * self.travel[0]
                self.has_moved[0] += 1
                self.vector[0] *= -1
            else:
                self.has_moved = [0, 0]
                self.speed -= 20
                if self.speed <= 100:
                    self.speed = 100
                self.time = GameState.alien_time

class Ammo(pygame.sprite.Sprite):
    def __init__(self, color, (width, height)):
        pygame.sprite.Sprite.__init__(self)
        self.image = pygame.Surface([width, height])
        self.image.fill(color)
        self.rect = self.image.get_rect()
        self.speed = 0
        self.vector = 0

    def update(self):
        self.rect.x += self.vector * self.speed
        if self.rect.y < 0 or self.rect.y > RES[1]:
            self.kill()

class Block(pygame.sprite.Sprite):
    def __init__(self, color, (width, height)):
        pygame.sprite.Sprite.__init__(self)
        self.image = pygame.Surface([width, height])
        self.image.fill(color)
        self.rect = self.image.get_rect()
```

> **整洁的代码**  
> 在这里清晰地标记所有最常用的全局变量，使得我们之后的代码更易于阅读。此外，如果我们想改变某个事物的大小，我们只需在这里修改，它就会在所有地方生效。

```python
class GameState:
    pass

class GameObject:
    def __init__(self):
        pygame.init()
        pygame.font.init()
        self.clock = pygame.time.Clock()
        self.game_font = pygame.font.Font('data/orbiter.ttf', 28)
        self.info_font = pygame.font.Font('data/orbiter.ttf', 72)
        self.screen = pygame.display.set_mode((RES[0], RES[1]))
        self.time = pygame.time.get_ticks()
        self.refresh_rate = 20
        self.rounds_won = 0
        self.level_up = 50
        self.score = 0
        self.lives = 2
        self.player_group = pygame.sprite.Group()
        self.alien_group = pygame.sprite.Group()
        self.bullet_group = pygame.sprite.Group()
        self.missile_group = pygame.sprite.Group()
        self.barrier_group = pygame.sprite.Group()
        self.all_sprite_list = pygame.sprite.Group()
        self.intro_screen = pygame.image.load('data/start_screen.jpg').convert()
        self.background = pygame.image.load('data/space_background.jpg').convert()
        self.image = pygame.image.load('data/ship.png').convert()
        self.alien_image = pygame.image.load('data/spaceship16.png').convert()
        GameState.alien_time = 0
        GameState.start_screen = True
        GameState.vector = 0
        GameState.shot_bullet = False

    def control(self):
        for event in pygame.event.get():
            if event.type == pygame.QUIT:
                GameState.start_screen = False
                GameState.end_game = True
            if event.type == pygame.KEYDOWN:
                if event.key == pygame.K_ESCAPE:
                    GameState.start_screen = False
                    GameState.end_game = True
                    self.kill_all()
                GameState.start_screen = True
            if self.keys = pygame.key.get_pressed()
            if self.keys[pygame.K_LEFT]:
                GameState.vector = -1
            elif self.keys[pygame.K_RIGHT]:
                GameState.vector = 1
            else:
                GameState.vector = 0
            if self.keys[pygame.K_SPACE]:
                if GameState.start_screen:
                    GameState.start_screen = False
                    self.lives = 2
                    self.score = 0
                    self.make_player()
                    self.make_defenses()
                    self.alien_wave()
                else:
                    GameState.shot_bullet = True

    def splash_screen(self):
        while GameState.start_screen:
            self.kill_all()
            self.screen.blit(self.intro_screen, [0, 0])
            self.screen.blit(self.intro_font.render('PLAYERS', 1, WHITE), (265, 120))
            self.screen.blit(self.font.render('PRESS SPACE TO PLAY!', 1, WHITE), (274, 191))
```

> **组**  
> 我们创建的这长串组本质上是集合。每次我们创建其中一个项目时，它都会被添加到集合中，以便可以轻松地进行碰撞测试和绘制。

> **控制**  
> 处理键盘输入是控制方法。它检查按键事件并根据我们是在开始屏幕还是在游戏中进行相应的操作。

> **雨弹**  
> Ammo 类简短而精炼。我们只需要几个初始属性，update 方法会检查它是否仍在屏幕上。如果不在，则会被销毁。

![](img/3b256f430f51c98f1315671f6e4eec19_120_0.png)

