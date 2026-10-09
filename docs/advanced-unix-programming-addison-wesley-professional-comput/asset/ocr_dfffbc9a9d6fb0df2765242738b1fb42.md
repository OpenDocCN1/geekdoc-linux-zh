# Dates and Times

# 61

`gettimeofday` is a higher-resolution alternative to `time`, but none of the other functions take a `struct timeval` as an argument. They’ll take the `tv_sec` field by itself, however, since it’s a `time_t`, and you can deal with the microseconds separately. All you can safely assume about the type `tv_usec` is that it’s a signed integer of some size. However, there is no reason for it to be any wider than 32 bits, as there are only 1,000,000 microseconds in a second, so casting the `tv_usec` field to a `long` will work fine. You can time an execution interval by bracketing it with two calls to `gettimeofday` and then use `difftime` on the `tv_sec` fields and naked subtraction on the `tv_usec` fields.

Some implementations (FreeBSD, Darwin, and Linux, but not Solaris) use the second argument to `gettimeofday` to return time-zone information, but that’s nonstandard. Most implementations indicate an error with a −1 return, and even set `errno`. Those that don’t, return zero always, so you can safely check the error return in all cases.

A `time_t` is always in terms of UTC, but broken-down time (`struct tm`) and strings can be in UTC or local time. It’s convenient to use local time when times are entered or printed out, and this complicates things. There must be some way for the computer to know what time zone the user is in and whether it is currently standard or daylight time. Worse, when printing past times, the computer must know whether it was standard or daylight time back *then*. The various functions concerned with local time deal with this problem fairly well.

The user’s time zone is recorded in the environment variable `TZ` or as a system default if `TZ` isn’t set. To provide portability, there’s one function and three global variables to deal with time-zone and daylight-time settings:

![](bbox=[0.15, 0.7, 0.86, 0.79])

An application can call `tzset` to somehow get the time zone (from `TZ` or wherever) and set the three globals, as follows: