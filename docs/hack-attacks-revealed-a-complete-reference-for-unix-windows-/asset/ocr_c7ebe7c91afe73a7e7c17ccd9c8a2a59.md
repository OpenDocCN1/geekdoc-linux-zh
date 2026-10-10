```
response->status_message = data;
log_verbose ("http_parse_response: status message = \"%s\"",
 response->status_message);
len += n;
n = read_until (fd, '\n', &data);
if (n <= 0)
{
http_destroy_response (response);
return n;
}
free (data);
if (n != 1)
{
log_error ("http_parse_request: invalid line ending");
http_destroy_response (response);
return -1;
}
len += n;
n = parse_header (fd, &response->header);
if (n <= 0)
{
http_destroy_response (response);
return n;
}
len += n;
*response_ = response;
return len;
}
void
http_destroy_response (Http_response *response)
{
if (response->status_message)
free ((char *)response->status_message);
http_destroy_header (response->header);
free (response);
}
static inline Http_request *
http_allocate_request (const char *uri)
{
Http_request *request;
request = malloc (sizeof (Http_request));
if (request == NULL)
return NULL;
request->uri = strdup (uri);
if (request->uri == NULL)
{
free (request);
return NULL;
}
return request;
}
Http_request *
```