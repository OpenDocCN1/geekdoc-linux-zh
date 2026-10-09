```
x1 = vidscape_vertices[x_v1];
y1 = vidscape_vertices[y_v0];
}else if(vidscape_vertices[x_v1] == vidscape_vertices[y_v1]) {
x0 = vidscape_vertices[x_v1];
y0 = vidscape_vertices[y_v0];
x1 = vidscape_vertices[x_v0];
y1 = vidscape_vertices[y_v1];
}else if(vidscape_vertices[x_v1] == vidscape_vertices[z_v1]) {
x0 = vidscape_vertices[x_v1];
y0 = vidscape_vertices[y_v1];
x1 = vidscape_vertices[x_v0];
y1 = vidscape_vertices[y_v0];
}else {
fprintf(stderr,"fatal error: origin not found");
}

if ( vidscape_vertices[x_v0] == vidscape_vertices[z_v0] ) {
z0 = vidscape_vertices[z_v0];
z1 = vidscape_vertices[z_v1];
}else if(vidscape_vertices[x_v0] == vidscape_vertices[z_v1]) {
z0 = vidscape_vertices[z_v1];
z1 = vidscape_vertices[z_v0];
}else if(vidscape_vertices[x_v0] == vidscape_vertices[z_v0]) {
z0 = vidscape_vertices[z_v0];
z1 = vidscape_vertices[z_v1];
}else if(vidscape_vertices[x_v1] == vidscape_vertices[z_v1]) {
z0 = vidscape_vertices[x_v1];
z1 = vidscape_vertices[z_v0];
}else {
fprintf(stderr,"fatal error: origin not found");
}
pos = X0;
x_axis.x = x1.x - x0.x;
x_axis.y = x1.y - x0.y;
x_axis.z = x1.z - x0.z;
y_axis.x = y1.x - x0.x;
y_axis.y = y1.y - x0.y;
y_axis.z = y1.z - x0.z;
z_axis.x = z1.x - x0.x;
z_axis.y = z1.y - x0.y;
z_axis.z = z1.z - x0.z;

int dummy1,dummy2,dummy3;
fgets(vidscape_line, 1024, fp);
sscanf(vidscape_line, "%d %d %d", &dummy1, &dummy2, &dummy3);
fgets(vidscape_line, 1024, fp);
sscanf(vidscape_line, "%d %d %d", &dummy1, &dummy2, &dummy3);

found = 1;
int done = 0;
int shift=0;
oid = 0;
while(!feof(fp) && !done) {
fgets(vidscape_line, 1024, fp);
if(!feof(fp)) {
sscanf(vidscape_line,
"%d %d %d",
&v_ytxcount, &v_vtx0_0, &v_vtx0_1);
if(v_ytxcount != 2) {
```