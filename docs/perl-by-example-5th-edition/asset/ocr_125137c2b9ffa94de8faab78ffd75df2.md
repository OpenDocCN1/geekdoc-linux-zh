and then,

```
podchecker path/Module.pm
```

and hope that it displays the following:

```
path/Module.pm pod syntax OK.
```

# Table 14.3 pod commands

| Paragraph Commands | What They Do |
| :--- | :--- |
| `=pod` | Marks the start of pod, but an equal sign, followed by any pod instruction starts the documentation. |
| `=cut` | Marks the end of pod. |
| `=head1 heading` | Creates a level1 heading. |
| `=head2 heading` | Creates a level2 heading. |
| `=item *` | Starts a bulleted list. |
| `=over N` | Moves over N number of spaces, usually set to 4. |
| `=back` | Returns indent back to default, no indent. |

| Formatting Commands | What They Do |
| :--- | :--- |
| `I<text>` | Creates italic text. |
| `B<text>` | Creates bold text. |
| `S<text>` | Contains text nonbreaking spaces. |
| `C<code>` | Contains typed text, literal source code. |
| `L<name>` | Creates a link (cross reference) to name. |
| `F<file>` | Used for listing filenames. |
| `X<index>` | An index entry. |
| `Z<>` | A zero-width character. |

| Filter-Specific Commands | What They Do |
| :--- | :--- |
| `=for` | For HTML-specific commands; e.g., `=for html <IMG SRC=file.gif> <B>Figure a.</B>>` |
| | For text-specific commands; e.g., `=for text` |
| | For manpage-specific commands; e.g., `=for man_ce 3 <center next three lines>` |