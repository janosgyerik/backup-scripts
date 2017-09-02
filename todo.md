next
----

- add plugin help, including description, triggered by -h appearing anywhere after plugin name; this is important, because it's not obvious what kind of parameters are required by mysql and paths plugins

later
-----

- add -lh flags for list command
  - workaround: ./backups.sh list | xargs ls -lh
- add logging for cron command
  - update the crontab to redirect cron command output to logs/daily.log
- add proper tests with multiple arguments in xoo

framework improvements
----------------------

- create daily/monthly/weekly/hourly crontabs to reduce the workload of the cron command -- but maybe this is unnecessarily complex, the current slowness is probably not a big concern in practice
- store the periods in a more convenient format, for example space separated list of terms: daily weekly monthly hourly
  - the input format could stay the same, for easy processing and compact writing

design goals
------------

- organize backups by label, a slug, for example bashoneliners
- possible to add new kind of backup (db, files, dirs, web) without modifying base script
- default periods are daily, monthly, weekly, hourly
- do not dump a database 3 times just to create 3 different periods, dump once and reuse
  - not very important: in a serious deployment, use a serious tool
  - can be mitigated by tuning the timing of jobs in the crontab
