
```
598

## response->status_message = data;

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
```
```
void

http_destroy_response (Http_response *response)

{

if (response->status_message)

free ((char *)response->status_message);

http_destroy_header (response->header);

free (response);

}
```
```
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
```
```
Http_request *

http_create_request (Http_method method,

                   const char *uri,

                   int major_version,

                   int minor_version)

{

  Http_request *request;

  request = http_allocate_request (uri);

  if (request == NULL)

    return NULL;

  request->method = method;

  request->major_version = major_version;

  request->minor_version = minor_version;

  request->header = NULL;

  return request;

}
```
```
ssize_t

http_parse_request (int fd, Http_request **request_)

{

  Http_request *request;

  unsigned char *data;

  size_t len;

  ssize_t n;

  *request_ = NULL;

  request = malloc (sizeof (Http_request));

  if (request == NULL)

    {

      log_error ("http_parse_request: out of memory");

      return -1;

    }

  request->method = -1;

  request->uri = NULL;

  request->major_version = -1;

  request->minor_version = -1;

  request->header = NULL;

  n = read_until (fd, ' ', &data);

  if (n <= 0)

    {

      free (request);

      return n;

    }

  request->method = http_string_to_method (data, n - 1);

  if (request->method == -1)

    {

      log_error ("http_parse_request: expected an HTTP method");

      free (data);

      free (request);

      return -1;

    }

  data[n - 1] = 0;

  log_verbose ("http_parse_request: method = \"%s\"", data);

  free (data);

  len = n;

  n = read_until (fd, ' ', &data);

if (n <= 0) {

free (request);

return n;

}

data[n - 1] = 0;

request->uri = data;

len += n;

log_verbose ("http_parse_request: uri = \"%s\"", request->uri);

n = read_until (fd, '/', &data);

if (n <= 0) {

http_destroy_request (request);

return n;

}

else if (n != 5 || memcmp (data, "HTTP", 4) != 0) {

log_error ("http_parse_request: expected \"HTTP\\\"");

free (data);

http_destroy_request (request);

return -1;

}

free (data);

len = n;

n = read_until (fd, '.', &data);

if (n <= 0) {

http_destroy_request (request);

return n;

}

data[n - 1] = 0;

request->major_version = atoi (data);

log_verbose ("http_parse_request: major version = %d", request->major_version);

free (data);

len += n;

n = read_until (fd, 'r', &data);

if (n <= 0) {

http_destroy_request (request);

return n;

}

data[n - 1] = 0;

request->minor_version = atoi (data);

log_verbose ("http_parse_request: minor version = %d", request->minor_version);

free (data);

len += n;

n = read_until (fd, '\n', &data);

if (n <= 0) {

http_destroy_request (request);

        return n;

    }

    free (data);

    if (n != 1)

      {

        log_error ("http_parse_request: invalid line ending");

        http_destroy_request (request);

        return -1;

      }

    len += n;

    n = parse_header (fd, &request->header);

    if (n <= 0)

      {

        http_destroy_request (request);

        return n;

      }

    len += n;

    *request_ = request;

    return len;

}
```
```
ssize_t

http_write_request (int fd, Http_request *request)
```
