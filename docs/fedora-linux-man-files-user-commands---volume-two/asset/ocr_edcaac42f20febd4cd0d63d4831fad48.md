# CONFIGURATION

core.notesRef
Notes ref to read and manipulate instead of refs/notes/commits. Must be an unabbreviated ref name. This setting can be overridden through the environment and command line.

notes.displayRef
Which ref (or refs, if a glob or specified more than once), in addition to the default set by core.notesRef or GIT_NOTES_REF, to read notes from when showing commit messages with the git log family of commands. This setting can be overridden on the command line or by the GIT_NOTES_DISPLAY_REF environment variable. See (1).

notes.rewrite.<command>
When rewriting commits with <command> (currently amend or rebase), if this variable is false, git will not copy notes from the original to the rewritten commit. Defaults to true. See also “notes.rewriteRef” below.
This setting can be overridden by the GIT_NOTES_REWRITE_REF environment variable.

notes.rewriteMode
When copying notes during a rewrite, what to do if the target commit already has a note. Must be one of overwrite, concatenate, and ignore. Defaults to concatenate.
This setting can be overridden with the GIT_NOTES_REWRITE_MODE environment variable.

notes.rewriteRef
When copying notes during a rewrite, specifies the (fully qualified) ref whose notes should be copied. May be a glob, in which case notes in all matching refs will be copied. You may also specify this configuration several times.
Does not have a default value; you must configure this variable to enable note rewriting.
Can be overridden with the GIT_NOTES_REWRITE_REF environment variable.