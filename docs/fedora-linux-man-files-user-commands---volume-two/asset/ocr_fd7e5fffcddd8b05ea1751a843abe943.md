# SPECIFYING REFERENCES

git bundle will only package references that are shown by git show-ref: this includes heads, tags, and remote heads. References such as master~1 cannot be packaged, but are perfectly suitable for defining the basis. More than one reference may be packaged, and more than one basis can be specified. The objects packaged are those not contained in the union of the given bases. Each basis can be specified explicitly (e.g. ^master~10), or implicitly (e.g. master~10..master, —since=10.days.ago master).

It is very important that the basis used be held by the destination. It is okay to err on the side of caution, causing the bundle file to contain objects already in the destination, as these are ignored when unpacking at the destination.