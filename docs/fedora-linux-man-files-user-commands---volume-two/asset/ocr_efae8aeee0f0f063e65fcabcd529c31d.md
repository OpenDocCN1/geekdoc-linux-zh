# SUBMODULES

If the patch contains any changes to submodules then *git apply* treats these changes as follows.

If —index is specified (explicitly or implicitly), then the submodule commits must match the index exactly for the patch to apply. If any of the submodules are checked-out, then these check-outs are completely ignored, i.e., they are not required to be up-to-date or clean and they are not updated.

If —index is not specified, then the submodule commits in the patch are ignored and only the absence or presence of the corresponding subdirectory is checked and (if possible) updated.