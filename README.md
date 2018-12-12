# Maillog: a Postfix log analyzer

## Translation note

What follows is an approximated translation of the original README file, which was written in russian (it is now renamed as ``README_ru.md``).

## Introduction

When the mail server processes the email, it broke down the transaction across several lines into the log file. In case of large mail traffic, the lines related to different email are mixed up, sometimes the records related to one email are several dozen lines apart. This greatly hinders reading the logs. In order to solve this problem, some time ago I wrote a script in Perl with the original name ``maillog``. Over time, functionalities were added to it and bugs were fixed.

## Options

The script scans the log files, grouping the lines by email. Entries are highlighted in color depending on the success of the delivery, addresses are highlighted.

It is possible to filter messages by sender and/or receiver with the ``-f`` and ``-t`` options, respectively.

Using the ``-d`` option, it is possible to set the date or a range of dates on which to display email. Dates can be set in different formats, for example:

* 12.1.2010-15.1.2010 - show email from the 12th to the 15th inclusive. 
* January 10, 2010 - show email from the 10th and later. 
* 12.01 - the opposite of the previous format, till the 12th and earlier. 

If year or month is omitted, then the current ones are substituted. In general, all that was '1.1.2010' is intended as 'January 1, 2010'. By default, email are displayed only for the current day.

If you want to see only email with errors, i.e. which have not been delivered, you can use the ``-e`` option.

All listed options can be used in any combinations.

There is support for log files compressed after rotation.

## Limitations

Only date and month are written in logs, therefore it is impossible to filter email by year. You can always omit the year with the -d option. If anyone has a thought, write to me.

My month is written in English in the log Jan, Feb, etc., if someone has them in Russian, add Russian elements to the ``%MONTHS`` hash.

The script works only with Postfix logs. I do not remember now that logs from other servers are very different, it is possible to actually add support for other programs.

## How to use the script

``maillog [-F mail*.log] [-d DATE] [-f FROM] [-t TO] [-e] [-h] [-V]``

Shows the entries in the mail log for letters coming from the FROM address to the TO address for the period specified in the DATE option.

```
    -F which files have to be parsed.

    -f FROM mailing address of the sender (or part of it).

    -t TO mailing address of the recipient (or part thereof).

    -d DATE to print the report for the specified period, if the option is skipped, only entries for the current day are displayed.

        DD/MM/YY-DD/MM/YY Full format:

        -DD/MM/YY Missing start date:
                            entries from January 1, 1970 will be shown.

        DD/MM/YY- Missing end date:
                            entries up to the current date are displayed.

        - Missing both the start and end dates:
                            entries from January 1, 1970 to current date.

    -e show only undelivered messages.

    -h show help page.

    -V show program version and license.
```

## GPLv2 license

This program is free software; you can redistribute it and/or modify it under the terms of the Free Software Foundation; either version 2, or (at your option) any later version.
