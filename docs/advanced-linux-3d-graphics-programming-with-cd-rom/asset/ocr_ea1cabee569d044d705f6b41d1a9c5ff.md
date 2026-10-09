```
```cpp
vidscape_vertices[v vtx0_0].z==
vidscape_vertices[x_v1].z)
&&
(vidscape_vertices[v_vtx0_1].x==
vidscape_vertices[x_v0].x &&
vidscape_vertices[v_vtx0_1].y==
vidscape_vertices[x_v0].y &&
vidscape_vertices[v_vtx0_1].z==
vidscape_vertices[x_v0].z));

oid |= bit<<shift;
shift++;
}
}

sprintf(attrib_frame, "%%s%s.lu.dat",
config->obj_path.c_str());
blender_config->ATTRIB_FILENAME,
oid);
this->current_id = oid;
}

lineno++;
}
fclose(fp);
if(!found) {
int magic_vtx_ctr;
for(magic_vtx_ctr=0; magic_vtx_ctr < 4*2; magic_vtx_ctr+=2) {
sprintf(vidscape_line, "2 %d %d 0x%x",
num_vertices+magic_vtx_ctr, num_vertices+magic_vtx_ctr+1,
0x0);
vidscape_string=vidscape_line;
new_vidscape_strings.push_back(vidscape_line);
}
int stop=magic_vtx_ctr + 3*2;
for(; magic_vtx_ctr < stop; magic_vtx_ctr+=2) {
sprintf(vidscape_line, "2 %d %d 0x%x",
num_vertices+magic_vtx_ctr, num_vertices+magic_vtx_ctr+1,
0x0);
vidscape_string=vidscape_line;
new_vidscape_strings.push_back(vidscape_line);
}
stop=magic_vtx_ctr + 2*2;
for(; magic_vtx_ctr < stop; magic_vtx_ctr+=2) {
sprintf(vidscape_line, "2 %d %d 0x%x",
num_vertices+magic_vtx_ctr, num_vertices+magic_vtx_ctr+1,
0x0);
vidscape_string=vidscape_line;
new_vidscape_strings.push_back(vidscape_line);
}
unsigned long temp_oid = oid;
while(temp_oid) {
```
```