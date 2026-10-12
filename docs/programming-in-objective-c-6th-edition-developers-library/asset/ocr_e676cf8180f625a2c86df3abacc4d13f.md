```
return 0; } struct time timeUpdate (struct time now) { ++now.seconds; if ( now.seconds == 60 ) { // next minute now.seconds = 0; ++now.minutes; if ( now.minutes == 60 ) { // next hour now.minutes = 0; ++now.hour; if ( now.hour == 24 ) // midnight now.hour = 0; } } return now; }
```