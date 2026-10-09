
# 第4 章：3D 视觉与感知

```c
#include <stdlib.h>

#include <stdio.h>

#include "../lib/2d/screen.h"

#include "../lib/system/dispatch.h"

#include "../lib/raster.h"
```

```cpp
#include "../lib/system/factorys.h"

#define MAXDOTS 500

#define NEARDOTS_INTERVAL 1

#define MEDDOTS_INTERVAL 2

#define FARDOT_INTERVAL 4

// STEP 1: CHOOSE THE FACTORIES

void choose_factories(void) {

    factory_manager_v_0_1.choose_factories();

}

// STEP 2: DECLARE PIPELINE SUBCLASS

class my_pipeline : public 13d_pipeline {

protected:

    13d_rasterizer2d_imp *ri;

    13d_rasterizer2d *r;

    unsigned long color;

    int neardots[MAXDOTS], neardots_y, neardots_x_spacing, neardots_ctr;

    int meddots[MAXDOTS], meddots_y, meddots_x_spacing, meddots_ctr;

    int fardots[MAXDOTS], fardots_y, fardots_x_spacing, fardots_ctr;

    int num_neardots, num_meddots, num_fardots;

public:

    13d_screen *s;

    my_pipeline();

    virtual ~my_pipeline();

    void key_event(int ch); // from dispatcher

    void update_event(void); // from dispatcher

    void draw_event(void); // from dispatcher

};

my_pipeline::my_pipeline() {

    s = factory_manager_v_0_1.screen_factory->create(320,200);

    ri = factory_manager_v_0_1.ras_2d_imp_factory->create(320,200,s->sinfo);

    r = new 13d_rasterizer2d(ri);

    s->sinfo->ext_max_green = 255;

    s->sinfo->ext_max_blue = 254;

    s->sinfo->ext_to_native(0, 0, 0); // allocate black background color

    s->refresh_palette();

    int i, x;

    neardots_y = 180;

    neardots_x_spacing=20;

    neardots_ctr = NEARDOTS_INTERVAL;

    for(i=0,x=0; x<320 && i < MAXDOTS; i++) {

        neardots_x[i] = x;

        x+=neardots_x_spacing;

    }

    num_neardots=i;

}

/* Middle row of runway lights */
```

```c
meddots_y = 140;           /* 中行：在屏幕上靠上 */

meddots_x_spacing=10;      /* 中行：中等间距 */

meddots_ctr = MEDDOTS_INTERVAL;      /* 中行：中等速度 */

/* 在给定的间距内，一行挤入尽可能多的灯 */

for(i=0, x=0; x<320 && i < MAXDOTS; i++) {

    meddots_x[i] = x;

    ++meddots_x_spacing;

}

num_meddots=1;

/* 跑道的远端 */             /* 远行：在屏幕靠上方 */

n_fardots_y = 120;           /* 远行：间距密集 */

n_fardots_ctr = FARDOTS_INTERVAL;      /* 远行：移动缓慢 */

/* 在给定的间距内，一行挤入尽可能多的灯 */

for(i=0, x=0; x<320 && i < MAXDOTS; i++) {

    n_fardots_x[i] = x;

    ++n_fardots_x_spacing;

}

num_n_fardots=1;
```

```cpp
my_pipeline::my_pipeline(void) {

    delete s;

    delete ri;

    delete r;

}

void my_pipeline::key_event(int ch) {

    switch(ch) {

        case 'q': {

            exit(0);

        }

    }

}

void my_pipeline::update_event() {

    int i;

    /* 移动所有点 */

    neardots_ctr--;

    if (neardots_ctr == 0) { /* neardots 每隔 NEARDOT_INTERVAL 移动一次 */

        neardots_ctr = NEARDOT_INTERVAL;

        for(i=0;i<num_neardots;i++) {

            neardots_x[i]--;

            if(neardots_x[i]<0) neardots_x[i] += 320;

        }

    }

    meddots_ctr--;

    if (meddots_ctr == 0) { /* meddots 每隔 MEDDOTS_INTERVAL 移动一次 */

        meddots_ctr = MEDDOTS_INTERVAL;

        for(i=0;i<num_meddots;i++) {

            meddots_x[i]--;

            if(meddots_x[i]<0) meddots_x[i] += 320;

        }

    }

    n_fardots_ctr--;

    if (n_fardots_ctr == 0) { /* fardots 每隔 FARDOTS_INTERVAL 移动一次 */

        n_fardots_ctr = FARDOTS_INTERVAL;

        for(i=0;i<num_n_fardots;i++) {

            n_fardots_x[i] -=;

            if(n_fardots_x[i]<0) n_fardots_x[i] += 320;

        }

    }

}

void my_pipeline::draw_event(void) {

    int i;

    r->clear_buffer();

    r->plot all dots();

    for(i=0; i<num_neardots; i++) {

        r->draw_point(neardots_x[i],neardots_y,color);

    }

    for(i=0; i<num_meddots; i++) {

        r->draw_point(meddots_x[i],meddots_y,color);

    }

    for(i=0; i<num_n_fardots; i++) {

        r->draw_point(n_fardots_x[i],n_fardots_y,color);

    }

    s->blit_screen();

}
```

```c
main() {

    choose_factories();

    3d_dispatcher *d;

    my_pipeline *p;

    // 步骤 3: 创建一个调度器

    d = factory_manager_v_0_1.dispatcher_factory->create();

    // 步骤 4: 创建流水线

    // - 将我们自定义的行为流水线插入调度器

    p = new my_pipeline();

    // 步骤 5: 调度器

    d->pipeline = p; // 多态赋值

    d->event_source = p->s;

    d->start();

    delete d;

    delete p;

}
```
