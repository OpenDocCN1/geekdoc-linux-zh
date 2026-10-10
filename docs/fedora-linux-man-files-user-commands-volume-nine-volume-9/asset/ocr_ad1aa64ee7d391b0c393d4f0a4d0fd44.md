# ENVIRONMENT

$$SYSTEMD\_EDITOR

Editor to use when editing units; overrides $EDITOR and $VISUAL. If neither $SYSTEMD\_EDITOR nor $EDITOR nor $VISUAL are present or if it is set to an empty string or if their execution failed, systemctl will try to execute well known editors in this order: (1), (1), (1), (1).

$$SYSTEMD\_PAGER

Pager to use when —**no-pager** is not given; overrides $PAGER. Setting this to an empty string or the value “cat” is equivalent to passing —**no-pager**.

$$SYSTEMD\_LESS

Override the default options passed to **less** (“FRSXMK”).