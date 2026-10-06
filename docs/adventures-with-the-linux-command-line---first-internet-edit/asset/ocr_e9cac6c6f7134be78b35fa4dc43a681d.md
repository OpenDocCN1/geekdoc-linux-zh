```
set -g default-terminal "screen-256color"

# Make copy work like vi
# Start copy 'b-
# Use vi movement keys (arrows, etc.)
# Select with V, y
# Yank and copy mode with y
# Paste with 'b-
# View all key bindings with 'b-: followed by list-keys -T copy-mode-vi
set-window-option -g mode-keys vi
bind-key -T copy-mode-vi 'v' send -X begin-selection
bind-key -T copy-mode-vi 'y' send -X copy-selection-and-cancel
```

# byobu

byobu (pronounced "BEE-oh-boo") from the Japanese word for "a folding, decorative, multi-panel screen" is not a terminal multiplexer se, but rather, it is a wrapper around either GNU screen or tmux (the default is tmux). It aims to create a simplified user interface with an emphasis on presenting useful system information on the status bar.

# Availability

byobu was originally developed by Canonical employee Dustin Kirkland, and as such is usually found in Ubuntu and other Debian-based distributions. Recent versions are more portable than the initial release, and it is beginning to appear in a wider range of distributions. It is distributed as the package "byobu".

# Invocation

byobu can be launched simply by entering the command byobu followed optionally by any options and commands to be passed to the backend terminal multiplexer (i.e., tmux or screen). For this adventure, we will confines our discussion to the tmux backend as it supports a larger feature set.