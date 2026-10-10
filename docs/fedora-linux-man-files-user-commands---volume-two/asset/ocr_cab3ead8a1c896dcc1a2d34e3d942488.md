Show colored diff. —color (i.e. without =<when>) is the same as —color=always. <when> can be one of always, never, or auto. It can be changed by the color.ui and color.diff configuration settings.

—no-color

Turn off colored diff. This can be used to override configuration settings. It is the same as —color=never.

—word-diff[=<mode>]

Show a word diff, using the <mode> to delimit changed words. By default, words are delimited by whitespace; see —word-diff-regex below. The <mode> defaults to plain, and must be one of:

+   color
+   Highlight changed words using only colors. Implies —color.

+   plain
+   Show words as [-removed-] and {+added+}. Makes no attempts to escape the delimiters if they appear in the input, so the output may be ambiguous.

+   porcelain
+   Use a special line-based format intended for script consumption. Added/removed/unchanged runs are printed in the usual unified diff format, starting with a +/-/` character at the beginning of the line and extending to the end of the line. Newlines in the input are represented by a tilde `~` on a line of its own.

+   none
+   Disable word diff again.

Note that despite the name of the first mode, color is used to highlight the changed parts in all modes if enabled.

—word-diff-regex=<regex>

Use <regex> to decide what a word is, instead of considering runs of non-whitespace to be a word. Also implies —word-diff unless it was already enabled.

Every non-overlapping match of the <regex> is considered a word. Anything between these matches is considered whitespace and ignored(!) for the purposes of finding differences. You may want to append [[^:space:]] to your regular expression to make sure that it matches all non-whitespace characters. A match that contains a newline is silently truncated(!) at the newline.

The regex can also be set via a diff driver or configuration option, see (1) or (1). Giving it explicitly overrides any diff driver or configuration setting. Diff drivers override configuration settings.

—color-words[=<regex>]