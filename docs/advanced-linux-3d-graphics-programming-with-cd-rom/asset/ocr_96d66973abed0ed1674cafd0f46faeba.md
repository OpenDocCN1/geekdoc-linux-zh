```
    }
prev_v_vtxcount = v_vtxcount;
prev_v_vtx0_0 = v_vtx0_0;
prev_v_vtx0_1 = v_vtx0_1;
}

if(overlapping_edge_count==4)
{

    int x_v0, x_v1,
    y_v0, y_v1,
    z_v0, z_v1;

    fgetc(vidscape_line, 1024, fp);
    sscanf(vidscape_line, "%d %d %d", &v_vtxcount, &x_v0, &x_v1);
    fgetc(vidscape_line, 1024, fp);
    sscanf(vidscape_line, "%d %d %d", &v_vtxcount, &y_v0, &y_v1);
    fgetc(vidscape_line, 1024, fp);
    sscanf(vidscape_line, "%d %d %d", &v_vtxcount, &z_v0, &z_v1);

    int dummy1,dummy2,dummy3;
    fgetc(vidscape_line, 1024, fp);
    sscanf(vidscape_line, "%d %d %d", &dummy1, &dummy2, &dummy3);
    fgetc(vidscape_line, 1024, fp);
    sscanf(vidscape_line, "%d %d %d", &dummy1, &dummy2, &dummy3);

    found = 1;
    int done = 0;
    int shift=0;
    oid = 0;
    while(!feof(fp) && !done) {
        fgetc(vidscape_line, 1024, fp);
        if(!feof(fp)) {
            sscanf(vidscape_line,
            "%d %d %d", &v_vtxcount, &v_vtx0_0, &v_vtx0_1);
        if(v_vtxcount != 2) {  
            done=1;
        }else {

            int bit = !
                (((vidscape_vertices[v_vtx0_0].x==
                vidscape_vertices[x_v0].x &
                vidscape_vertices[v_vtx0_0].y==
                vidscape_vertices[x_v0].y &
                vidscape_vertices[v_vtx0_0].z==
                vidscape_vertices[x_v0].z
                &
                (vidscape_vertices[v_vtx0_1].x==
                vidscape_vertices[x_v1].x &
                vidscape_vertices[v_vtx0_1].y==
                vidscape_vertices[x_v1].y &
                vidscape_vertices[v_vtx0_1].z==
                vidscape_vertices[x_v1].z))
                ||
                ((vidscape_vertices[v_vtx0_0].x==
                vidscape_vertices[x_v1].x &
                vidscape_vertices[v_vtx0_0].y==
```