![](bbox=[0.2, 0.11, 0.46, 0.3])

![](bbox=[0.49, 0.11, 0.75, 0.3])

*Figure 7-9: Using line-of-sight to control lens flare.*

![](bbox=[0.2, 0.38, 0.46, 0.58])

![](bbox=[0.49, 0.38, 0.75, 0.58])

*Figure 7-10: Using distance to control lens flare.*

# ## Particle Systems

A *particle system* is a system of many small objects, called *particles*, all of which are set into motion and controlled by some algorithm specific to the system. Any effect which can be viewed as a collection of particles can be modeled with a particle system. Examples of systems that can be modeled with particle systems are explosions, fire, smoke, a swarm of insects, or a school of swimming fish.

The particles in a particle system are typically numerous, ranging from the hundreds to the thousands. It is the collective optical effect of all the particles as a whole system that leads to the term particle system. Because the effect depends on the quantity of particles, it is often the case that the particles themselves are very simple objects. They can be actual polygonal objects (as with a school of fish), or simple billboards (for fire or smoke), or even simply single points (for explosions or insect swarms). The simpler the representation, the more particles you can have in the system. Speed is also of primary concern in a real-time particle system, because there are so many particles.