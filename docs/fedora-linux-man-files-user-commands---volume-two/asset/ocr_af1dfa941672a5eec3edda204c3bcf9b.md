of the commit object name in "describe" output, even when the commit in question happens to be a tagged version. Instead of just emitting the tag name, it will describe such a commit as v1.2.0-gdeadbee (0th commit since tag v1.2 that points at object deadbee... ).

+   —match <pattern>

Only consider tags matching the given (7) pattern, excluding the "refs/tags/" prefix. This can be used to avoid leaking private tags from the repository.

+   —always

Show uniquely abbreviated commit object as fallback.

+   —first-parent

Follow only the first parent commit upon seeing a merge commit. This is useful when you wish to not match tags on branches merged in the history of the target commit.