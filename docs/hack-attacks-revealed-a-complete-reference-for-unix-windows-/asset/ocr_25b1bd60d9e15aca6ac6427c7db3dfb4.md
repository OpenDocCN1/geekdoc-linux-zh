```
if (buf2 == NULL)

log_error ("read_until: realloc: shrink failed"); /* not fatal

*/

else

buf = buf2;

*data = buf;

return len;

}

static inline Http_header *

http_alloc_header (const char *name, const char *value)

{

Http_header *header;

header = malloc (sizeof (Http_header));

if (header == NULL)

return NULL;

header->name = header->value = NULL;

header->name = strdup (name);

header->value = strdup (value);

if (name == NULL || value == NULL)

{

if (name == NULL)

free ((char *)name);

if (value == NULL)

free ((char *)value);

free (header);

return NULL;

}

return header;

}

Http_header *

http_add_header (Http_header **header, const char *name, const char

*value)

{

Http_header *new_header;

new_header = http_alloc_header (name, value);

if (new_header == NULL)

return NULL;

new_header->next = NULL;

while (*header)

header = &(*header)->next;

*header = new_header;

return new_header;

}

static ssize_t

parse_header (int fd, Http_header **header)

{

unsigned char buf[2];

unsigned char *data;

Http_header *h;

size_t len;

ssize_t n;

*header = NULL;
```