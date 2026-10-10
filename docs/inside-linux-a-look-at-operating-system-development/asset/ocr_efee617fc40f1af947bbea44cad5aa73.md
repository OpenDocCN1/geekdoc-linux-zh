# 5.1. USER INTERFACE

# 5.1.1 Defining System Calls

Writing a standards document is not an easy task. The standard must find a balance between describing what must be done without describing how it should be implemented. In addition, it is very easy to rely on unwritten assumptions which may not be shared by someone who later reads the standard. Thus, it is probably not a good idea to have the same person define the calls and implement the system. It is also a good idea to open the documentation process to a large number of people with differing viewpoints. The resulting contrasts will highlight elements of the standard which must be clarified¹.

One major issue in writing a standard is deciding if the standard is to be *permissive* or *restrictive*. A permissive standard describes a set of behaviors that are sufficient and necessary to claim conformance. Such a standard allows extensions. A restrictive standard describes a set of behaviors that must be met exactly to claim conformance. Such a standard prohibits extensions.

There are several schools of thought with respect to extensions. When applications rely on extensions to the system kernel, those applications may be “locked into” that specific implementation. Programmers who rely on a wonderful extension provided by one vendor will later discover that they will have to incur large reprogramming costs to shift to a different vendor.

Another danger in a permissive standard is found in hidden features that are known only to a select few. “Undocumented calls” are an effective way to bind several applications together or to bind an application with an operating system. A competitor is then obliged to duplicate both applications or the application and the operating system. (These hidden features appear to be among the difficulties encountered on the WINE project.)

If extensions are disallowed or not used (or not provided), applica-

> ¹This effort can be quite formal. For instance, there was a test called WierdNIX. As part of the evaluation of the Trial Use Standard, the IEEE 1003 Working Group offered prizes for the best new and technically legal interpretation of the POSIX standard which nevertheless violates the intuitive intent of the POSIX standard[3].