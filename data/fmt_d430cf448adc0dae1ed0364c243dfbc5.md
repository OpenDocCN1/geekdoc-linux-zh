
### AIModule

包含每个单位移动的逻辑。

某些单位（如陆陆器）正在寻找可以接的人。变异人追捕玩家。导弹只会一直飞行直到死亡，等等。

```c
void AIMModule(typUnit *unit)
{
    typUnit *tmp;
    int bestdest = 50000;
    typUnit *closest = NULL;
    GLList *node;

    /*
     * 外星陆陆器 AI 逻辑
     */
    if (unit->type == LANDER) {
        /* ... 如果外星人锁定了某人 ... */
        if (unit->lockunit) {
            /* -- 向上移动 -- */
            closest = unit->lockunit;
            unit->y -= .5;
            closest->y -= .5;
            /* -- 如果外星人到达顶部 -- */
            if (unit->y - (sprite_lander->height / 2) < RADAR_HEIGHT) {
                /* -- 同化人类！ -- */
                unit->y = RADAR_HEIGHT + (sprite_lander->height / 2);
                unit->type = MUTANT;
                unit->pctFiring = MUTANT_PCT;
                unit->lockunit = NULL;
                closest->bDestroy = TRUE;
            }
        }
        return;
    }

    /* ... 附近有可以抓取的吗？ ... */
    for (node = unitList; node = node->next) {
        tmp = (typUnit *)node->data;
        if (tmp->type == PERSON && tmp->lockunit == NULL) {
            /* 寻找更近的人 -- */
            if (DistanceBetween(unit, tmp) < bestdest) {
                closest = tmp;
                bestdest = DistanceBetween(unit, tmp);
            }
        }
    }

    /* --- 我们锁定了目标 --- */
    if (bestdest <= 1) {
      /* ... 移动一点 ... */
      unit->vx = 0;
      unit->x = closest->x;
      /*
       * 检查锁定 ...
       */
      if ((unit->y + (sprite_lander->height / 2)) < (closest->y - (sprite_man->height / 2))) {
        /* ... 向它降临 ... */
        unit->y += .5;
      } else if ((unit->y + (sprite_lander->height / 2)) > (closest->y + (sprite_man->height / 2))) {
        unit->y -= .5;
      } else {
        /* ... 锁定 ... */
        unit->lockunit = closest;
        closest->lockunit = unit;
        closest->life = 20;
      }
      /* --- 在合理范围内吗？ --- */
    } else if (bestdest < 20) {
      /* ... 向它移动 ... */
      unit->vx = Direction(unit, closest);
      unit->x += unit->vx;
    } else {
      /*
       * 附近没有。随机方向移动。
       */
      if (unit->vx == 0) {
        if ((rand() % 2) == 0) {
          unit->vx = 1;
        } else {
          unit->vx = -1;
        }
      }
      unit->x += unit->vx;
    }

    /* 最后移动单位 --- */
    Move(unit);
    /* 让变异人尝试射击 --- */
    AttemptFiring(unit);

    /*
    * 导弹和爆炸
    */
    else if (unit->type == MISSILE || unit->type == EXPLOSION) {
      /* --- 它们有寿命。减1 --- */
      unit->life -= 1;
      /* --- 移动它 --- */
      Move(unit);
      /* --- 当寿命归零时销毁它 --- */
      if (unit->life <= 0) {
        unit->bDestroy = TRUE;
      }
    }

    /* 人类 AI */
    else if (unit->type == PERSON) {
      /*
      * 只有当它的外星人被击中
      * 从天空掉落时，人才自己移动。
      */
      if (unit->lockunit == NULL && unit->y < PERSON_HEIGHT) {
        /* --- 向下移动 --- */
        unit->y += 2;
      }
    }
}
```

### GetSprite

获取单位的精灵图（素材）。

```c
typSprite *GetSprite(typUnit *unit) {
    typSprite *sprite;

    /* --- 获取素材 --- */
    switch (unit->type) {
        case HERO:
            sprite = sprite_ship;
            break;
        case PERSON:
            sprite = sprite_man;
            break;
        case LANDER:
            sprite = sprite_lander;
            break;
        case MUTANT:
            sprite = sprite_mutant;
            break;
        case MISSILE:
        case EXPLOSION:
            sprite = sprite_missile;
            break;
        default:
            sprite = NULL;
            break;
    }

    return (sprite);
}
```

### AnyoneBetween

这些坐标之间有单位吗？激光在计算是否击中时使用。

```c
typUnit *AnyoneBetween(int x1, int y1, int x2, int y2) {
    GLList *node;
    typUnit *unit;
    typUnit *closestUnit = NULL;
    int closestX;
    typSprite *sprite;
    int screenX;

    /* 检查每个单位 --- */
    for (node = unitList; node = node->next) {
        unit = (typUnit *)node->data;
        /* 如果是坏人 --- */
```
