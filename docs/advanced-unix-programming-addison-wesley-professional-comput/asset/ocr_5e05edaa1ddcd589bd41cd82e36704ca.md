# Table A.1 Process Attributes (cont.)

| Attribute | fork | exec | Section |
| :--- | :--- | :--- | :--- |
| directory, current | copied | preserved | 3.6.2 |
| directory, root | copied | preserved | 5.14 |
| exit status¹ | - | - | 5.7 |
| file descriptions | shared | unchanged | 2.2 |
| file descriptors | copied | preserved unless FD_CLOEXEC set | 2.2 |
| file locks | not copied | preserved unless fd was closed | 7.11 |
| file-mode creation mask | copied | preserved | 2.4.2 |
| floating-point environment² | copied | default | - |
| ID, effective group | copied | depends on set-group-ID bit | 5.12 |
| ID, effective user | copied | depends on set-user-ID bit | 5.12 |
| ID, parent process | changed | preserved | 5.13 |
| ID, process | new | preserved | 5.13 |
| ID, process-group | copied | preserved | 4.3 |
| ID, real group | copied | preserved | 5.12 |
| ID, real user | copied | preserved | 5.12 |
| ID, saved set-group-ID | copied | depends on set-group-ID bit | 5.12 |
| ID, saved set-user-ID | copied | depends on set-user-ID bit | 5.12 |
| ID, thread (thread) | copied | lost | 5.17.1 |
| ID, supplementary group | copied | preserved | 1.1.8 |
| limit, resources (incl. file size) | copied | preserved | 5.16 |