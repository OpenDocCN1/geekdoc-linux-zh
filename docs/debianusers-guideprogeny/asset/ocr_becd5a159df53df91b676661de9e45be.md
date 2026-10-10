The first three entries should always be the Identifier, Horizsync, and VertRefresh.

For a complete list of settings, see the man page for the XF86Config.

> Warning Never edit a monitor profile without consulting the monitor's documentation. Settings that are too high for the monitor can damage it or prevent it from working.

# ## Monitor Settings

| Setting | Comments |
| :--- | :--- |
| Identifier | The name for this monitor profile. |
| HorizSync | The horizontal scanning frequency. Usually, this is a range. 30-130 should work for most monitors. |
| VertRefresh | The vertical scanning frequency. Usually, this is a range. 60-160 should work for most monitors |
| Gamma | Set the gamma correction for the monitor. In order, settings are listed for red, green and blue, using RGB values. |