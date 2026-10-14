Top-Down commands (Table 14-1) are designed to take a lot of the complexity out of working with LSM. With one command (volassist), you can create a volume that consists of two striped plexes.

As you become more comfortable with LSM, you may find that the Top-Down commands are a little

# LSM Top-Down Commands

| Command | Location | Man | Type | Description |
|---|---|---|---|---|
| volassist | /sbin | 8 | binary | Program to create, mirror, back up, grow, shrink, and move LSM volumes. |
| voldiskadd | /usr/sbin | 8 | sh | Adds one or more disks for use within LSM. |
| voldisksetup | /usr/sbin | 8 | sh | Sets up a disk for use within LSM. |
| volevac | /usr/sbin | 8 | sh | Evacuates all volumes from a disk. |
| volmirror | /usr/sbin | 8 | sh | Mirrors volumes on a disk or control default mirroring. |

# Table 14-1: LSM Top-Down Commands

# LSM Bottom-UP Commands

| Command | Location | Man | Type | Description |
|---|---|---|---|---|
| voldg | /sbin | 8 | binary | Manages LSM disk groups. |
| voldisk | /sbin | 8 | binary | Creates and manages LSM disks. |
| voledit | /sbin | 8 | binary | Creates, removes, and modifies LSM records. |
| volmake | /sbin | 4/8 | binary | Creates LSM objects. This is an advanced command that can be used to create many LSM objects quickly. It looks like a top-down command when run, but the preparation is definitely more of a bottom-up approach. Very powerful. |
| volmend | /usr/sbin | 8 | binary | Repairs (mends) simple problems in LSM configuration records. |
| volplex | /sbin | 8 | binary | Manages LSM plexes. |
| volsd | /sbin | 8 | binary | Manages LSM subdisks. |
| volume | /sbin | 8 | binary | Manages LSM volumes. |

# Table 14-2: LSM Bottom-Up Commands