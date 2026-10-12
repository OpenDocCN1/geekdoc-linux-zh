
```python
self.refresh_screen()
    pygame.time.delay(3000)
    return True
```

```python
def calc_collisions(self):
    pygame.sprite.groupcollide(self.missile, self.barrier_group, True, True)
    pygame.sprite.groupcollide(self.player, self.barrier_group, False, True)
```

```python
def make_defenses(self):
    for i, spacing in enumerate(range(0)):
        make_barrier(3, 9, spacing)
        barrier.rect.x = 450 + (i * 10)
        self.barrier_group.add(barrier)
        self.all_sprites.add(barrier)
```

```python
def kill_all(self):
    for items in [self.bullet, self.player_group, self.alien_group, self.missile_group]:
        for i in items:
            i.kill()
```

```python
self.score += 10
    if pygame.sprite.groupcollide(self.player, self.alien_group, False, True):
        self.lives -= 1
        self.lives -= 1
```

```python
def is_dead(self):
    if self.lives < 0:
        self.screen.blit(self.game_font.render("战争输了！你的得分为 " + str(self.score), True, (255, 255, 255)), (250, 250))
        self.refresh_screen()
        pygame.time.delay(3000)
        return True
```

```python
def next_round(self):
    for alien in self.alien_group:
        alien.wave_level(self.level)
    make_defenses(self)
    self.level += 50
```

```python
def win_round(self):
    if len(self.alien_group) < 1:
        self.rounds_won += 1
        self.screen.blit(self.game_font.render("你赢得了这一回合战斗！" + str(self.rounds_won), True, (0, 255, 0)), (200, 250))
        self.refresh_screen()
        pygame.time.delay(3000)
        return True
```

```python
    while not Game.state.end_game:
        Game.game_time = pygame.time.get_ticks()
        Game.state.alien_time = pygame.time.get_ticks()
        self.control():
            self.make_missile()
        for alien in self.alien_group:
            alien.move()
```

```python
def defenses_breached(self):
    for alien in self.alien_group:
        if alien.rect.bottom > 410:
            self.screen.blit(self.game_font.render("外星人突破了地球", True, (255, 0, 0)), (180, 155))
```

```python
        if self.Game_shoot:
            self.make_bullet()
        self.calc_collisions(self)
        if self.is_dead() or self.defenses_breached():
            Game.state.end_game = True
        if self.win_round():
            self.next_round()
            self.refresh_screen()
            self.splash_screen()
            pygame.quit()
```

```python
if __name__ == '__main__':
    game = Game()
    game.main_loop()
```

![](img/c72194f2c3aec1989366a5167c92_0.png)

# 使用 Python 创建《太空入侵者》克隆版

## 太空入侵者第 2 部分：图形与声音

### 你需要...

- Raspian

  www.raspberry.org/downloads

- Python

  www.python.org/docs

- Pygame

  www.pygame.org/docs

- Art assets

  opengame.org

## 太空入侵者第 2：图形与声音

这一次我们将扩展《太空入侵者》克隆版，包含沉浸式动画和声音。

在之前的教程中，我们创建了基础的《太空入侵者》克隆版，由于 Pygame 的组管理和碰撞检测能力，这为我们的项目带来了巨大的变化。不仅在代码长度上，如果你错过了第一部分，可以通过 GitHub 找到 v0.1 代码列表，而你可以找到 v0.2 代码，包含了所有的图像、音乐和音效。

为了帮助你保持项目易于管理和遵循代码，我们在 `Game` 类中集成了一些动画方法并使用了精灵图（sprite sheet）。这不仅让绘制屏幕变得非常简单，还保持了计数性能，这对于树莓派尤其重要。我们希望你喜欢使用我们的技术为项目添加动画和声音！

![](img/c72194f2c3aec1989366a5167c93_0.png)

## 设置依赖

01 你可以通过下载代码来获得更多练习。无论你只是只想运行代码，都需要一些基础依赖。这两项要求是 Pygame 和 Git，它们都是默认安装的。这很简单！

## 下载依赖

02 Git 是一个优秀的版本控制系统，帮助程序员保存代码和文件。它不仅可以保留更改历史，意味着你可以从 GitHub 等地方克隆整个项目。要克隆本教程项目的最新版本，从命令行进入文件夹并输入：

## 导航项目

03 在 `pivaders` 文件夹中，readme 文件包含主游戏文件 `game.py`。你会找到图形和声音的子文件夹，以及用于标题屏幕的字体。要进行测试，只需进入子目录 (`cd pivaders`)，并使用方向键左右移动，使用空格键射击。你可以按 Escape 键退出。

```
git pull https://github.com/russ/pivadars
```

这将创建文件夹。

![](img/c72194f2c3aec1989366a5167c93_1.png)

## 太空入侵者第 2 部分：图形与声音

## 使用 Python 创建

### 代码列表（从...行开始）
