# Chapter 10: Basic Scripting and Forms

| Variable | Description |


| SERVER_ADMIN | The e-mail address of the Web server administrator. Use this in scripts to enable your scripts to send messages to the Web master about errors that occur during script processing. |

| REQUEST_METHOD | How the script data was passed. Usually either GET or POST. |

| HTTP_REFERR | The URL of the document from which the script was called (if included by the browser). |

| HTTP_USER_AGENT | A description of the browser name, platform, and version number, as provided by the browser with its request. |

| SCRIPT_NAME | The name of the script that was requested by the browser. |

| QUERY_STRING | The data passed as part of the URL (the part following the question mark), in encoded form, using plus signs and percentage signs for nonstandard characters. |

| REMOTE_HOST | The hostname of the computer that sent this request (if sent by the browser). |

| REMOTE_ADDRESS | The IP address of the computer making this request (if sent by the browser or resolvable by the Web server). |

| CONTENT_TYPE | The MIME type of the HTML form sent with a POSTed reply. |

| CONTENT_LENGTH | The number of bytes contained in a POSTed reply. |

| HTTP_ACCEPT | A list, separated by commas, of MIME types that the browser making this request can accept. |

# Reviewing Sample Script Fragments

Rather than presenting a complete script that will perform an event you may never need to use, this section includes several basic tasks that all scripts need to do, with a brief explanation of each and a Perl script for each task.

Every script will follow roughly the following series of steps, with some steps skipped depending on the data that the script gathers and the HTML pages that it responds to:

+   1. Check which method was used to call the script by querying the REQUEST_METHOD variable.

+   2. Get the submitted data from the QUERY_STRING (for GET) or from the Standard Input (for POST).