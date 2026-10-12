| 405 | Module 10.4.6 | Method Not Allowed |
| --- | --- | --- |
| 406 | Module 10.4.7 | Not Acceptable |
| 407 | Module 10.4.8 | Proxy Authentication Required |
| 408 | Module 10.4.9 | Request Timeout |
| 409 | Module 10.4.10 | Conflict |
| 410 | Module 10.4.11 | Gone |
| 411 | Module 10.4.12 | Length Required |
| 412 | Module 10.4.13 | Precondition Failed |
| 413 | Module 10.4.14 | Request Entity Too Large |
| 414 | Module 10.4.15 | Request-URI Too Large |
| 415 | Module 10.4.16 | Unsupported Media Type |
| 416 | Module 10.4.17 | Requested Range Not Satisfiable |
| 417 | Module 10.4.18 | Expectation Failed |
| Server Error - the server failed to fulfill an apparently valid request |  |  |  |
| 500 | Module 10.5.1 | Internal Server Error |
| 501 | Module 10.5.2 | Not Implemented |
| 502 | Module 10.5.3 | Bad Gateway |
| 503 | Module 10.5.4 | Service Unavailable |
| 504 | Module 10.5.5 | Gateway Timeout |
| 505 | Module 10.5.6 | HTTP Version Not Supported |
| Extended error messages |  |  |  |
| xxx | see below |  |  |

HTTP status codes are extensible, i.e. a server can generate response codes other than the ones listed in the table. HTTP applications are not required to understand the meaning of all registered status codes, although such understanding is obviously desirable. However, applications must understand the class of any status code, as indicated by the first digit, and treat any unrecognized response as being equivalent to the x00 status code of that class, with the exception that an unrecognized response must not be cached. For example, if an unrecognized status code of 431 is received by the client, it can safely assume that there was something wrong with its request and treat the response as if it had received a 400 status code. In such cases, user agents should present to the user the entity returned with the response, since that entity is likely to include human-readable information that will explain the unusual status.