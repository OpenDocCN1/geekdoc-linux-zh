
然后，我们只需在适当的时候触发音效。以激光为例，我们希望每当按下空格键射击时就播放，因此我们将它放在`Game`类的`Control`方法中，就在设置`shoot_bullet`标志之后。

如果你难以找到免费且开放的音效，我们推荐`www.freesound.org`。

```python
self.player_group.add(self.player)
self.all_sprite_list.add(self.player)

def refresh_screen(self):
    self.all_sprite_list.draw(self.screen)
    self.animate_player()
    self.player_explosion()
    self.alien_explosion()
    self.refresh_scores()
    pygame.display.flip()
    self.screen.blit(self.background, [0, 0])
    self.clock.tick(self.refresh_rate)

def refresh_scores(self):
    self.screen.blit(self.game_font.render("SCORE " + str(self.game_score), 1, WHITE), (0, 0))
    self.screen.blit(self.game_font.render("LIVES " + str(self.lives) + " ", 1, RED), (355, 570))

def alien_wave(self, speed):
    for column in range(BARRIER_COLUMN):
        for row in range(BARRIER_ROW):
            alien = Alien()
            alien.rect.y = 65 + (column * (ALIEN_SIZE[1] + ALIEN_SPACER))
            alien.rect.x = ALIEN_SIZE[0] + ALIEN_SPACER + row * (ALIEN_SIZE[0] + ALIEN_SPACER)
            self.alien_group.add(alien)
            self.all_sprite_list.add(alien)
            alien.speed = speed

def make_bullet(self):
    if GameState.game_time - self.player.time > self.player.speed:
        bullet = Ammo(BLUE, BULLET_SIZE)
        bullet.vector = -1
        bullet.speed = 7
        bullet.rect.x = self.player.rect.x + 28
        bullet.rect.y = self.player.rect.y
        self.bullet_group.add(bullet)
        self.all_sprite_list.add(bullet)
        self.player.time = GameState.game_time
    GameState.shoot_bullet = False

def make_missile(self):
    if len(self.alien_group):
        shoot = random.choice()
        if shoot <= 0.05:
            shooter = random.choice([alien for alien in self.alien_group])
            missile = Ammo(RED, MISSILE_SIZE)
            missile.vector = 1
            missile.rect.x = shooter.rect.x + 15
            missile.rect.y = shooter.rect.y + 40
            missile.speed = 4
            self.missile_group.add(missile)
            self.all_sprite_list.add(missile)

def make_barrier(self, columns, rows, spacer):
    for column in range(columns):
        for row in range(rows):
            barrier = Block(WHITE, (BLOCK_SIZE))
            barrier.rect.x = 55 + (200 * spacer) + (row * 10)
            barrier.rect.y = 55 + (column * 10)
            self.barrier_group.add(barrier)
            self.all_sprite_list.add(barrier)

def make_defenses(self):
    for spacing, spacing in enumerate(range()):
        self.make_barrier(, 9, spacing)

def kill_all(self, self.bullet_group, self.player_group, self.alien_group, self.missile_group, self.barrier_group):
    for items in (self.bullet_group, self.player_group, self.alien_group, self.missile_group, self.barrier_group):
        for i in items:
            i.kill()

def is_dead(self):
    if self.lives < 0:
        self.screen.blit(self.game_font.render("The war is lost! You scored: " + str(self.score), 1, RED), (250, 15))
        self.rounds_won = 0
        self.refresh_screen()
        self.level_up = 50

self.explode = False
self.alien.explode = False
pygame.time.delay(300)
return True

def defenses_breached(self):
    for alien in self.alien_group:
        if alien.rect.y > ...:
            self.screen.blit(self.game_font.render("The aliens have breached Earth defenses!", 1, RED), (180, 15))
            self.refresh_screen()
            self.level_up = 50
            self.explode = False
            self.alien.explode = False
            pygame.time.delay(3000)
            return True

def win_round(self):
    if len(self.alien_group) < 1:
        self.rounds_won += 1
        self.screen.blit(self.game_font.render("You won round " + str(self.rounds_won) + " but the battle rages on!", 1, RED), (200, 15))
        self.refresh_screen()
        pygame.time.delay(3000)
        return True

def next_round(self):
    self.explode = False
    self.alien.explode = False
    for actor in [self.missile_group, self.barrier_group, self.bullet_group]:
        for i in actor:
            i.kill()
    self.alien_wave(self.level_up)
    self.make_defenses()
    self.level_up += 50

def calc_collisions(self):
    pygame.sprite.groupcollide(self.missile_group, self.barrier_group, True, True)
    pygame.sprite.groupcollide(self.bullet_group, self.barrier_group, True, True)
    for z in pygame.sprite.groupcollide(self.bullet_group, self.alien_group, True, True):
        self.alien.explode = True
        self.explode_alien.append(z.rect.x)
        self.explode_alien.append(z.rect.y)
        self.score += 10
        self.explosion_fx.play()
    if pygame.sprite.groupcollide(self.player_group, self.missile_group, False, True):
        self.lives -= 1
        self.explode = True
        self.explosion_fx.play()

def main_loop(self):
    while not GameState.end_game:
        while not GameState.start_screen:
            GameState.game_time = pygame.time.get_ticks()
            GameState.alien_time = pygame.time.get_ticks()
            self.control()
            self.make_missile()
            self.calc_collisions()
            self.refresh_screen()
            if self.is_dead() or self.defenses_breached():
                GameState.start_screen = True
            for actor in [self.player_group, self.bullet_group, self.alien_group, self.missile_group]:
                for i in actor:
                    i.update()
            if GameState.shoot_bullet:
                self.make_bullet()
            if self.win_round():
                self.next_round()
            self.splash_screen()
    pygame.quit()

if __name__ == '__main__':
    pv = Game()
    pv.main_loop()
```

# 使用 Python 制作视觉小说游戏

通过 Python 和 Pygame 创建互动小说或选择你自己的冒险，来弥合书籍与电子游戏之间的差距

![](img/3b256f430f51c98f1315671f6e4eec19_127_0.png)

切换场景以增加故事的深度，并允许游戏拥有决策和路线

### 资源

- **Python 2:** www.python.org/
- **Pygame:** pygame.org/download.shtml
- **IDLE Python IDE**
- **游戏素材**
- **来自 FileSilo 的代码（可选）**

大多数人会在现代电子游戏中寻找引人入胜的故事，而那些没有故事的游戏正变得越来越少。讲述纯粹故事的一种很好的方式是通过视觉小说类型，你可以用 Python 相对简单地制作一个。这些互动小说在日本是一种极受欢迎的娱乐形式，通常通过让玩家点击浏览故事并在过程中做出决策来体验不同的情节点和结局。

在 Python 中，这是一个相对简单的项目来创建，但通过添加 Pygame 模块我们可以让它变得更容易，并且对未来更具可扩展性。Pygame 提供了更好的图像和文本定位支持，创建显示窗口以及使用鼠标和键盘输入，从而简化了编码过程。

我们将使用标准 Python 2 编写代码，因此在编写、测试和编码时请确保在 IDLE 2 而不是 IDLE 3 中运行它。

#### 01 获取 Pygame 依赖项

为你的系统安装 Pygame 的最佳方式是编译它。为此你需要先安装正确的依赖项。打开终端并安装以下软件包，在 Ubuntu 中看起来像这样：
