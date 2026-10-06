# Chapter 23

# The zsh Shell

To wrap up our discussion on Linux shells, this chapter takes a look at the newest of them, the zsh shell. The zsh shell provides some amazing features, and sets the bar high for any future development. This chapter discusses what makes the zsh so unique, and walks you through the various features available for use in your zsh shell scripts.

| IN THIS CHAPTER |
| Introducing the zsh shell |
| The parts of the zsh shell |
| Writing scripts for zsh |

# History of the zsh Shell

The z shell (called zsh) is an open source Unix shell developed by Paul Falstad. It takes ideas from the Bourne, bash, ash, and tsh shells and adds many unique features to create a full-blown advanced shell designed for programmers.

Some of the features that make the zsh shell unique are:

+   - Improved shell option handling
- Shell compatibility modes
- Loadable modules

All of these features, loadable modules are the most advanced thought in shell design. As you've seen in the previous shell chapters, each shell contains a set of built-in commands that are available without the need of external utility programs. The benefit of built-in commands is execution speed. The shell doesn't have to load a utility program into memory before running it, the built-in commands are already in the shell memory, ready to go.