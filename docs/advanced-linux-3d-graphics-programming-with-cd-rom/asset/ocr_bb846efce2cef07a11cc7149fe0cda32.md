```
int i;

for(i=0; i<MAXDOTS; i++) {
    dots[i] = new dot_particle();
    dots[i]->place_dot();
}

numdots = MAXDOTS;

);

int main(int argc, char **argv) {

    choose_factors();

    l3d_dispatcher *d;
    my_pipeline *p;

    d = factory_manager_v_0_3::dispatcher_factory->create();
    p = new my_pipeline_particle();

    d->pipeline = p;
    d->event_source = p->s;
    d->start();

    delete d;
    delete p;

}
```

# Comments on the Sample Program’s Physics

There are actually several oversimplifications made to the physics modeling in this program. Just for starters, the particles have no mass or volume, and cannot interact with each other. Also, we wantonly fooled around with the particles’ positions and velocities whenever we found that they happened to be beneath the floor, instead of actually detecting and handling collisions. So, although each particle behaves in a mostly realistic manner, there are still several physics issues which have been vastly and incorrectly simplified in this example. (We briefly return to the topic of physics in Chapter 8.) This is one of the advantages of particle systems: you can use a simple particle system as a testbed for simple physics code, and even if the physics isn’t completely correct, with a particle system it still tends to look good due to the sheer number of particles. Handling physics correctly is more important when we have a few, large objects interacting with one another, when we are more likely to notice exactly how the objects behave.

# Some Ideas for You to Try

You might want to experiment with the particle system to try to create some more interesting effects. Some ideas are:

+   Allow the particles to interact with one another. For instance, assign each particle a magnetic attractive or repulsive force, which affects all other particles. This would require saving the previous state of all particles in an array, and then updating each particle based on the sum of all previous forces exerted by all particles.