# —tag-name-filter <command>

This is the filter for rewriting tag names. When passed, it will be called for every tag ref that points to a rewritten object (or to a tag object which points to a rewritten object). The original tag name is passed via standard input, and the new tag name is expected on standard output.

The original tags are not deleted, but can be overwritten; use “—tag-name-filter cat” to simply update the tags. In this case, be very careful and make sure you have the old tags backed up in case the conversion has run amok.

Nearly proper rewriting of tag objects is supported. If the tag has a message attached, a new tag object will be created with the same message, author, and timestamp. If the tag has a signature attached, the signature will be stripped. It is by definition impossible to preserve signatures. The reason this is “nearly” proper, is because ideally if the tag did not change (points to the same object, has the same name, etc.) it should retain any signature. That is not the case, signatures will always be removed, buyer beware. There is also no support for changing the author or timestamp (or the tag message for that matter). Tags which point to other tags will be rewritten to point to the underlying commit.

# —subdirectory-filter <directory>

Only look at the history which touches the given subdirectory. The result will contain that directory (and only that) as its project root. Implies the section called “Remap to ancestor”.

# —prune-empty

Some kind of filters will generate empty commits, that left the tree untouched. This switch allow git-filter-branch to ignore such commits. Though, this switch only applies for commits that have one and only one parent, it will hence keep merges points. Also, this option is not compatible with the use of —commit-filter. Though you just need to use the function `git_commit_non_empty_tree “$@”` instead of the git commit-tree “$@” idiom in your commit filter to make that happen.

# —original <namespace>

Use this option to set the namespace where the original commits will be stored. The default value is refs/original.

# -d <directory>

Use this option to set the path to the temporary directory used for rewriting. When applying a tree filter, the command needs to temporarily check out the tree to some directory, which may consume considerable space in case of large projects. By default it does this in the .git-rewrite/ directory but you can override that choice by this parameter.

# -f, —force

git filter-branch refuses to start with an existing temporary directory or when there