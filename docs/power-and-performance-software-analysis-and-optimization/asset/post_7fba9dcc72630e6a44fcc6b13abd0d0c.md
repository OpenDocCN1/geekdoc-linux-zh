
## 10.2 bugLE-18 185

- **stats_calls** Records the number of times each OpenGL function was executed per frame
- **stats_basic** Records general information, such as frame rate or frame time
- **showextensions** Records the extensions that are used

Each of these filterset record counters and some, that begin with the word show, automatically output some of their data to the logfile. The rest make the counters available for reporting and for custom statistics. The location of the log is controlled via the `log` filters, and the contents of the log is controlled via the `logstats` filterset. For example, considering the following chain:

```bash
$1 cat ~/.bugle/filters
2 chain examplechain
3 {
4 filteret stats_calls
5 filteret stats_calltimes
6 filteret stats_basic
7
8 logstats
9
10 show "average time per call" # provided by stats_calltimes
11 show "time in GL" # provided by stats_calltimes
12 show "frames per second" # provided by stats_basic
13 show "ms per frame" # provided by stats_basic
14 }
15 filteret log
16 {
17 filename "/tmp/bugle.log"
18
19 }
```

Line 1 begins the definition of a new chain, very creatively named examplechain, and thus will be invoked by defining `BUGLE_CHAIN=examplechain`. Lines 4 enable 6 filtersets, `stats_calls`, `stats_calltimes`, and `stats_basic`, for reporting data. Enabling these three filtersets does not automatically output any data, but instead enables the counters to be available. The actual reporting definition begins at line 8, with the configuration of the `logstats` filterset. Each of the text strings on lines 10 through 13 represent a predefined statistic that is calculated using counters exported from the filterset on lines 4 through 6. The definition of each of these statistics, in relation to the filter counters, can be found in the `${HOME}/.bugle/statistics` file. Finally, lines 15 through 18 define the `log` filterset output.

All of the statistics used in this example are part of the defaults provided with the library. The only requirement was copying the provided statistics file into $(HOME)/.bugle/statistics, Included below are some excerpts from that file, defining the formulas for calculating the logstats utilized above.

```bash
$ cat ~/.bugle/statistics
#
# Core statistics
#
# "frames per second" = d("frames") / d("seconds")
{
    precision 1
    label "fps"
}
# "ms per frame" = 1000 * d("seconds") / d("frames")
{
    precision 2
    label "ms/frame"
}
#
# Call time statistics
#
# "average time per call" = d("calltimes::*") / d("calls:*") * 1000
{
    precision 3
    label "*"
}
#
"time in GL" = d("calltimes:total") / d("seconds") * 1000
{
    precision 1
    label "*"
}
```

Once the filtered datasets and statistics have been configured, data collection can begin by utilizing the LD_PRELOAD mechanism described above. For example, in order to collect the data described in the examplechain chain for glxspheres64 program:

```bash
$ env LD_PRELOAD=/usr/local/lib/libbugle.so.10.0.1 \
> LD_LIBRARY_PATH=/usr/local/lib/ \
> BUGLE_CHAIN=examplechain \
> glxspheres64
Polygons in scene: 62464
ATTENTION: default value of option force_s3tc_enable overridden by
environment.
```

## 10.3 Apitrace 187

Visual ID of window: 0x20
Context is Direct
OpenGL Renderer: Mesa Intel(R) Sandybridge Mobile

As defined in the log filterset in the examplechain, the log is written to /tmp/bugle.log. Below is an excerpt from that log for:

```text
1 [INFO] logstats.average time per call: 0.000 glList (ms)
2 [INFO] logstats.average time per call: 0.001 glDrawBuffer (ms)
3 [INFO] logstats.average time per call: 0.001 glViewport (ms)
4 [INFO] logstats.average time per call: 0.000 glTranslatef (ms)
5 [INFO] logstats.average time per call: 0.000 glPopMatrix (ms)
6 [INFO] logstats.average time per call: 0.004 glCallLists (ms)
7 [INFO] logstats.average time per call: 0.001 glLoadIdentity (ms)
8 [INFO] logstats.average time per call: 0.001 glDisable (ms)
9 [INFO] logstats.average time per call: 0.001 glFrustum (ms)
10 [INFO] logstats.average time per call: 0.001 glPopAttrib (ms)
11 [INFO] logstats.average time per call: 0.000 glMaterialf (ms)
12 [INFO] logstats.average time per call: 0.835 glClear (ms)
13 [INFO] logstats.average time per call: 0.001 glClearDepth (ms)
14 [INFO] logstats.average time per call: 0.004 glRasterPos (ms)
15 [INFO] logstats.average time per call: 0.002 glRotaf (ms)
16 [INFO] logstats.average time per call: 0.874 glSwapBuffers (ms)
17 [INFO] logstats.average time per call: 0.001 glMatrixMode (ms)
18 [INFO] logstats.average time per call: 0.025 glCallList (ms)
19 [INFO] logstats.average time per call: 0.001 glClearColor (ms)
20 [INFO] logstats.average time per call: 0.000 glPushMatrix (ms)
21 [INFO] logstats.average time per call: 0.000 glColorf (ms)
22 [INFO] logstats.average time per call: 0.001 glPushAttrib (ms)
23 [INFO] logstats.time in GL: 97.9 %
24 [INFO] logstats.frames per second: 61.8 fps
25 [INFO] logstats.ms per frame: 16.17 ms/frame
```

## 10.3 APITRACE

Apitrace is a tool for tracing and profiling OpenGL and EGL function calls. The tool consists of a command-line interface, apitrace, and a QT-based graphical interface. With OpenGL, this is achieved by preloading an augmented OpenGL implementation before the dynamic linker loads the real OpenGL code.

One of the great features of Apitrace is its ability to reconstruct the OpenGL state machine per function call. This includes being able to view a screenshot of each frame, a screenshot of each texture, and a list of the changed OpenGL state variables. Additionally, the profiling view shows the per-call durations for both the CPU and GPU. Collection begins either with the apitrace trace <application> command, or through the graphical interface by selecting the Menu bar item, and choosing the New item. In both cases, this will produce a trace file, named in the format <application>.trace. For example:

```bash
$ apitrace trace glxspheres64
error: failed to determine elf class for glxspheres64,
assuming ELF64
Polygons in scene: 62464
apitrace: tracing to /home/jtk/glxspheres64.1
apitrace: redirecting open(libGL.so.1, 0x102)
ATTENTION: default value of option force_s3tc_enable overridden
by environment.
```

Visual ID of window: 0x20
Context is Direct
OpenGL Renderer: Mesa Intel(R) Sandybridge Mobile

At this point, the trace is ready for analysis. At any time, the trace can be replayed with the gltrace command. This command will rerun OpenGL command on the trace, allowing for more information to be collected, or for the trace to be run on any system or configuration.

Figure 10.1 illustrates the trace for glxspheres64 in the graphical interface. By default, the first-parameter OpenGL calls, and their parameters are listed with:

![](img/33fad1fa149d4f0cdd55ff2565970ab2_205_0.png)

FIGURE 10.1
QT trace for Apitrace.

![](img/33fad1fa149d4f0cdd55ff2565970ab2_206_0.png)

FIGURE 10.2
QT interface for Apitrace profiling.

OpenGL state and surfaces at each call can be obtained by opening the Trace menubar item and selecting the Lookup State entry. This will cause the trace to be retraced, either for the whole trace or up until the highlighted frame or call. Once this has completed, a sidebar will appear on the right-hand side of the screen containing the data.

Apart from reconstructing the OpenGL state, trace can also be profiled by opening the Trace menubar and selecting the Profile entry. This will again cause the trace to be retraced, and a window containing a timeline of CPU and GPU times will utilize. By highlighting over the entries, the relevant OpenGL information will be displayed. An example of this can be seen in Figure 10.2.

# REFERENCES 189

- Barnes, J., Pincharch, L., Vetter, D., 2012. Linux DRM Developer’s Guide. $[LINUX_SRC/](Documentation/DocBook/drm).
- Boll, A., Paul, B., Forbes, C., et al., 2014. Mesa 3D Environment Variables. http://www.mesa3d.org/envvars.html.
