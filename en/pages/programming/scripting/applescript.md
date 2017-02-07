#Applescript

## Progress bar
```
set n to 10set progress total steps to nset progress description to "Script Progress"set progress additional description to "This should be helpful"repeat with i from 1 to n	delay 1	set progress completed steps to iend repeat```