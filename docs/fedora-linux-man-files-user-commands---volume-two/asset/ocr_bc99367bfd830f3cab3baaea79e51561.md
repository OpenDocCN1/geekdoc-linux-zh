internal branch structure to have no files in it, allowing the frontend to subsequently add all interesting files from scratch.

```
'deleteall' LF
```

This command is extremely useful if the frontend does not know (or does not care to know) what files are currently on the branch, and therefore cannot generate the proper filedelete commands to update the content.

Issuing a filedeleteall followed by the needed filemodify commands to set the correct content will produce the same results as sending only the needed filemodify and filedelete commands. The filedeleteall approach may however require fast-import to use slightly more memory per active branch (less than 1 MiB for even most large projects); so frontends that can easily obtain only the affected paths for a commit are encouraged to do so.

# ## notemodify

Included in a commit <notes_ref> command to add a new note annotating a <commit-ish> or change this annotation contents. Internally it is similar to filemodify 100644 on <commit-ish> path (maybe split into subdirectories). It’s not advised to use any other commands to write to the <notes_ref> tree except filedeleteall to delete all existing notes in this tree. This command has two different means of specifying the content of the note.

External data format

The data content for the note was already supplied by a prior blob command. The frontend just needs to connect it to the commit that is to be annotated.

```
'N' SP <dataref> SP <commit-ish> LF
```

Here <dataref> can be either a mark reference (:<idnum>) set by a prior blob command, or a full 40-byte SHA-1 of an existing Git blob object.

Inline data format

The data content for the note has not been supplied yet. The frontend wants to supply it as part of this modify command.

```
'N' SP 'inline' SP <commit-ish> LF data
```