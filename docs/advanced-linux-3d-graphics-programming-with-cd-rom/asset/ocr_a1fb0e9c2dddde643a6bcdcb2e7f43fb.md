```
};

virtual -13d_camera_collidable(void) {};
virtual int update(void) {
    13d_collidable::old_position = VRP;
    int status=13d_moveable::update();
    13d_collidable::new_position = VRP;
    return status;
};

#end
```

# # Class l3d_world_portal_textured_lightmapped_obj_collider

Class l3d_world_portal_textured_lightmapped_obj_collider is not only the longest class name in the book, it is also a world which implements simple collision detection on the camera object, preventing the camera object from walking through walls. A crashing sound is played for every collision.

Member variable sound_client is a pointer to a sound client object, which knows how to interface to a sound server to play sounds.

The constructor deletes the camera object created by the base class constructor, and replaces it with a new camera of type l3d_camera_collidable, which can collide with the environment. It also creates a sound client and asks the sound client to establish a connection with a sound server. Currently the sound server is hard-coded to be on the local host at IP address 127.0.0.1 on the RPlay port 5556.

Overridden method load_from_file is essentially the same as the inherited version, except it creates polygons of type l3d_polygon_3d_textured_lightmapped_collidable while reading the world file.

Overridden method update_all implements collision detection and response between the camera and the geometry in the sector. First, we position all sector geometry into world space, then merge the polygon lists for the sector and any moveable plug-in objects it might contain. Then, we check the camera for collision against all polygons in the sector by calling method detect_collision_with against every polygon in the sector. The camera's inherited member variable prevent_collision is set to 1 during these collision checks, meaning that the camera's position is corrected so as not to collide with any polygon in the sector. Since correcting the camera's position with respect to one polygon might make the position invalid with respect to another polygon, we must again loop through all polygons whenever the camera's position has been corrected, eventually leading to a camera position not colliding with any polygon. If a collision was detected, we play a sound. Portal crossing is also newly implemented; a portal crossing is defined as a moving collision with a portal. Earlier, we explicitly searched for containment of the camera within all sectors to find out if the camera crossed into another sector. Now, we use the technique of collision detection; if the camera's line of movement crosses through a polygon portal, which we test using the ray-polygon test, we set the current sector to the sector on the other side of the crossed portal.