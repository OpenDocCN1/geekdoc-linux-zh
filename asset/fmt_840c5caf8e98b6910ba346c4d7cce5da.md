
# 编写一个太空际入侵者克隆游戏

## 使用 Python 创建

```python
GameState.start_screen = False

self.lives -= 1

self.score = 0

self.player.move()

self.defenses()
else:
    GameState.end = True
```

```python
self.screen.blit(self.game_font.render(
'SCORE ' + str(self.score), 1, WHITE), (100, 10))

self.screen.blit(self.game_font.render(
'LIVES ' + str(self.lives), 1, WHITE), (350, 55))
```

```python
def alien_wave(self, speed):
    for column in range(BARRIER):
        alien = Alien()
        alien.rect.x = 100 + column * ALIEN_SIZE
        alien.rect.y = 50
        self.all_sprite_list.add(alien)
        alien.python
```

```python
def draw_title(self):
    . = .
    ................
    self.screen.blit(self.game_font.render(
    'INVADERS', 1, WHITE), (265, 120))
```

![](img/f16311c48f0c39ab87b1836be5339b9e_90.png)

```python
missile.vector = 1
missile.rect.x = shooter.rect.x + 15
missile.rect.y = shooter.y + 40
missile.speed = 10
self.missile_group.add(missile)
self.all_sprite_list.add(missile)
```

```python
self.refresh_screen()
pygame.time.delay(3000)
return True
```

```python
def calc_colisions(self):
 pygame.sprite.groupcollide(
  self.missile_group, self.barrier_group,
  True, True
 )
```

```python
def make_barrier(self, columns, rows, spacer):
 for column in range(columns):
  for row in range(rows):
   barrier = Block(WHITE, BLOCK_SIZE)
   barrier.rect.x = 200 + (column * (50 + spacer))
   barrier.rect.y = 450 + (row * 10)
   self.barrier_group.add(barrier)
   self.all_sprite_list.add(barrier)
```

```python
pygame.sprite.groupcollide(
 self.bullet_group, self.barrier_group,
  False, True
 )
pygame.sprite.groupcollide(
  self.bullet_group, self.alien_group,
  False, True
 )
```

```python
def make_defense(self):
 for spacing, alien in enumerate(range(0)):
  self.make_barrier(3, 9, 9)
```

```python
self.score += 10
 pygame.sprite.groupcollide(
  self.player_group, self.alien_group,
  False, True
 )
self.lives -= 1
```

```python
def kill_alien(self):
 for items in [self.bullet_group, self.player_group]:
  self.alien_group.spritecollide(items, True)
  for i in range(1):
   i.kill()
```

```python
def next_round(self):
 for actor in [self.missile_group, self.barrier_group, self.bullet_group]:
  for i in range(1):
   i.kill()
 self.make_wave(self.level)
 self.make_defense(self)
 self.level += 50
```

```python
def is_dead(self):
 if self.lives < 0:
  self.screen.blit(self.game_font.render(
  "The game is lost! You scored " + str(self.score), 1, RED), (250, 150))
  self.refresh_screen()
  pygame.time.delay(3000)
  return True
```

```python
while not Game.end_game:
  while not Game.Start_screen:
   Game.alien_time = pygame.time.get_ticks()
  get_ticks()
```

```python
def win_round(self):
 if len(self.alien_group) < 1:
  self.screen.blit(self.game_font.render(
  "You won round " + str(self.rounds_won), +
  1, RED), (200, 180))
  self.refresh_screen()
  pygame.time.delay(3000)
  return True
```

```python
self.control()
 self.make_alien()
 for actor in [self.player_group, self.alien_group, self.message_group]:
  for i in range(1):
   i.update()
 if Game.Alien_bullet:
```

```python
def defenses_breached(self):
 for alien in self.alien_group:
  if alien.rect.y > 410:
   self.screen.blit(self.game_font.render(
    "The aliens have breached Earth!"
    1, RED), (180, 155))
```

```python
if Game.Alien_bullet:
  self.calc_colisions()
 if self.is_dead() or defenses_breached():
  Game.Start_screen = True
 if self.win_round():
  self.next_round()
  self.splash_screen()
pygame.quit()
```

```python
if __name__ == '__main__':
 pv = Game()
 pv.main_loop()
```
