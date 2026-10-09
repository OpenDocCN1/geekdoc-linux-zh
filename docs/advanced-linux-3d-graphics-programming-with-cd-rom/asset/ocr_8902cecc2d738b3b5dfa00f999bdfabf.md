```
rand()\hs1->ext_max_blue);
}

if (objects[numm]==NULL) exit;
objects[numm]->modeling_xforms[1].set
(int_to_13d_real(1), int_to_13d_real(0), int_to_13d_real(0), int_to_13d_real(1),
int_to_13d_real(0), int_to_13d_real(1), int_to_13d_real(0), int_to_13d_real(1),
int_to_13d_real(0), int_to_13d_real(0), int_to_13d_real(1), int_to_13d_real(1),
int_to_13d_real(0), int_to_13d_real(0), int_to_13d_real(0), int_to_13d_real(1) );
objects[numm]->modeling_xform =
objects[numm]->modeling_xforms[0] ;
}
screen->refresh_palette();

main() {
13d_dispatcher *d;
13d_pipeline_world *p;
my_world *w;

factory_manager_v_0_2::choose_factories();
d = factory_manager_v_0_2::dispatcher_factory->create();

w = new my_world();
p = new 13d_pipeline_world(w);
d->pipeline = p;
d->event_source = w->screen;

d->start();

delete d;
delete p;
delete w;
}
```

# # Rotoscoping and Inverse Kinematics

Blender offers an interesting feature which can make creating IK animations easier. This feature is called rotoscoping. Rotoscoping is the use of live video material to assist in creating computer animations. Blender’s support for rotoscoping allows individual frames of a movie file to be synchronized with the Blender animation frame. The movie image is superimposed on top of the 3DWindow. Changing the Blender animation frame with the arrow keys also changes the displayed frame of the movie. For instance, moving ahead five animation frames in Blender also moves ahead five frames in the movie.

The idea is that the movie footage shows the movement of a character (e.g., a human) from a fixed camera position. Then, the 3D camera in Blender should be placed in a position in space corresponding to the position of the real movie camera used to take the video footage. The virtual camera and the real camera then view the scene from the same position. Rotoscoping work is thus done in Blender in the camera view (key 0 on the numeric keypad). For each frame of animation, we position the lkas such that the apparent position of the lkas in Blender’s camera view is identical to the apparent position of the real actor’s arms and legs in the real movie footage. This