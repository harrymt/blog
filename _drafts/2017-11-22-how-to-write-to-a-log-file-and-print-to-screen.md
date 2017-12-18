---
layout: post
title: How to write to a log file and print to screen with bash
---

<div class="message">
Bash script to write to a file and print to standard input.
</div>

## How to write to a log file and output to console.

Use `tee` like:

```bash
exec > >(tee -i "file.log")
exec 2>&1
echo "Prints to screen and file"
```

For example, a full script would be:


```bash
#!/bin/bash

#
# Create timestamp for use with filenames.
#
# Usage: echo "Hiya" > "$(create_filename).txt"
# 
# Returns: Saves "Hiya" to a txt file with current date time,
# e.g. 17-10-17-14:28:49.txt
time_filename()
{
    date +'%d-%m-%y-%s'
}


LogOutput="${1:-"./log"}"

# Setup Log
Log_file="$LogOutput/$(time_filename).log"
if [ ! -d "$LogOutput" ]; then
    echo "$(t_warn) dir $LogOutput does not exist! Trying to create it..."
    if mkdir -p "$LogOutput" ; then
        echo "$(t) successfully created dir $LogOutput"
    else
        exit 1
    fi
fi

exec > >(tee -i "$Log_file")
exec 2>&1

echo "Writing to log file: [ $Log_file ]"
```
