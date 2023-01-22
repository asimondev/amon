# Free Oracle Performance Tool AMON

## DESCRIPTION

*AMON* is a free performance monitoring tool for Oracle databases. The
tool is written in C using Oracle OCI API and UNIX Curses library.

This allows *AMON* to run on every UNIX terminal. After downloading this tool,
you can immediately start to use it. If **SQL*Plus** can run, then *AMON* should
execute as well. It's recommended to use local internal connect as SYSDBA
user. (**ORACLE_SID** environment variable should be set.)

## Interactive mode:
   **amon** -i interval -w window -S sid -P pid -f filter -b {y|n}
     -u user -p password -d database -r {sysdba | sysoper | sysasm}
     --pdb PDB -a directory -A minutes -e {b|t|a}
     -h -v -D {1|4|8|12|1000} -l {y|n} --color {dark | light | custom}

## Reporting mode:
   **amon** {-o report type | -O report type | -t[m][r] "name1, name2, .."}
     -i interval -c count -C paging -f filter -S sid -P pid
     --rows N -s {logreads | preads | pwrites | redo | wait_time}
     -u user -p password -d database -r {sysdba | sysoper | sysasm}
     --pdb PDB -h -v  
     --output-format {default|json} --output-file FileName
     --start-time YYYY-MM-DD HH:MM[:SS] --duration Minutes
     -D {1|4|8|12|1000} -l {y|n}

## Help parameters:
   **amon** -h [ { help (this text!) | -Opt | options | intro | all } ]

## OPTIONS

* `-A` <minutes>:
  ASH interval in minutes (interactive mode only). The default value is 60 minutes.

* `-a` <output directory>: AMON writes the output files to the current directory, if this parameter isn't specified (interactive mode only).

* `-b` <{y|n}>: Some terminal fonts don't support drawing the lines (interactive mode only). In this case you can use the option -b n to avoid drawing the boxes around the edges of a window. The default option is -b n.

* `-C` <number>: Number of iterations before the report header (column names) should be repeated (reporting mode only). The value 0 forces only the first page header. The default value depends on the specified report.

* `-c` <{count | NNm | NNh }>: Number of updates in reporting mode. If no
count is specified, then the default value is infinity. You can use the modifiers "m" and "h" to specify the AMON run time in minutes or hours.

* `-D` <{1 | 4 | 8 | 12 | 1000}>: This option activates AMON debug mode. The debug levels 1, 4, 8 and 12 starts Oracle SQL tracing with the corresponding trace level (debug event 10046). The AMON debug level 1000 produces a trace file
amon_sqls.log, which contains all issued SQL statements with bind variables values.

* `-d` <database alias>: Per default AMON will try to connect to the local instance using the ORACLE_SID environment variable. With the -d option
you can specify any other database to connect. The database alias can be
either TNS alias or Easy Connect string.

* `e` <{b|t|a|d}> : Execution plan format for the SQL cursor, which is saved into the file from the session view (z) window (interactive mode only). The default value is "t" (TYPICAL).Other possible values are "b" (BASIC), "a" (ALL) and "d" (ADVANCED). These are the possible format values for the used procedure
DBMS_XPLAN.DISPLAY_CURSOR to get the plan.

* `-f` <filter expression [-f filter expression]>: See amon-filter(7) for
more information on this option.

* `-i` <interval>: Refreshing interval in seconds. The minimal value is 2 seconds.
The default value is 10 seconds.

* `-l` <{y|n}>: Using of separately licensed Oracle Database options and
management packs. If you don't want to use ASH and Real-time
SQL monitoring, then you should specify the option "n" here.

* `-O` <report type [--short]>: This reporting mode uses the same reporting options as "-o" but produces a "grepable" output. Every output row starts with a time stamp and instance ID for a RAC database.

* `-o` <report type [--short]>: Use this option to write the statistics to the standard output. Some of the reports can provide statistics both for a local instance and for all RAC instances. You should use "r" modifier for a RAC report and "m" modifier for multitenant report.  

* `--short`* This option is only available for "rai" report.  
* `--rows` <N>: This option is only available for "s", "ss", "ee" reports.  
* `--start-time` <YYYY-MM-DD HH:MM[:SS]>: Set report start time.  
* `--duration` <Minutes>: Set the run-time report duration in minutes. 
* `--output-format` <format>: Available report formats are *default* and *json*. Currently this 
option only works for baseline system statistics report.  
* `--output-file` <Filename>: Report file name. Currently this option is not implemented for all 
available reports.  

Available ASM report types are:  
`D[r]`: Client disk I/O statistics (V$ASM_DISK_IOSTAT).  
`L[r]`: Active long running operations (V$ASM_OPERATION).  
`d[r]`: Disk I/O statistics (V$ASM_DISK).  

Available RDBMS report types are:  
`B[r]`:    Automatic big table caching details.  
`D`:       Disk I/O statistics for database files.  
`E[r]`:    System wait events.  
`EEE[r]`:  CDB System wait events.  
`I`:       I/O statistics.  
`II`:      Disk I/O statistics for database functions.  
`L[r]`:    Running long operations.  
`P[r]`:    Session memory details.  
`R[r]`:    Recovery details (V$RECOVERY_PROGRESS).  
`RR[r]`:   Recovery processes (V$RECOVERY_SLAVE).  
`TT[r]`:   Active transactions (V$TRANSACTIONS).  
`U[r]`:    Redo dest. histograms (V$REDO_DEST_RESP_HISTOGRAM).  
`UU`:      Redo apply histograms (V$STANDBY_EVENT_HISTOGRAM).  
`a[m][r]`: Sampled session activity (V$ACTIVE_SESSION_HISTORY).  
`as[r]`:   Session details from ASH (V$ACTIVE_SESSION_HISTORY).  
`aa[r]`:   Archived log details (V$ARCHIVED_LOG).  
`d`:       Datafiles I/O statistics.  
`dd`:      Tempfiles I/O statistics.  
`dnfs[r]`: Direct NFS statistics (V$DNFS_STATS).  
`e`:       Grouped session wait events (V$SESSION_WAIT).  
`ee[r]`:   Session wait events (V$SESSION_WAIT).  
`g`:       General database information and redo logs switches.  
`gg[r]`:   General CDB details (V$PDBS).  
`gz`:      Database parameters (V$SYSTEM_PARAMETER).  
`l[r]`:    Blocked session details (V$SESSION_BLOCKER).  
`m`:       Memory allocation (SGA + PGA).  
`mm[r]`:   In-Memory column store details (V$IM_SEGMENTS).  
`p[r]`:    Parallel execution processes.  
`pp[r]`:   AUTO parallel degree policy execution.  
`rai[r]`:  RMAN performance details (V$BACKUP_ASYNC_IO).  
`rsi[r]`:  RMAN performance details (V$BACKUP_SYNC_IO).  
`s[r]`:    Session statistics (program, service, etc).  
`ss[r]`:   Session statistics (wait events, etc.).  
`sq[r]`:   Session and SQL statistics. -S or -P options are allowed.  
`sa`:      ASH samples for the specified session (-S or -P options).  
`se`:      Session events for the specified session (-S or -P options).  
`st`:      Session time statistics for the specified session (-S or -P options).  
`sz`:      One-time statistic snapshot for a specific session.  
`t[r]`:    System time model statistics.  
`tt[r]`:   Session time model statistics.  
`ttt[r]`:  CDB system time model statistics.  
`uuu[r]`:  Standby details from V$MANAGED_STANDBY.  
`uuu2[r]`: Standby details from V$DATAGUARD_STATS.  
`uuu3[r]`: Data Guard messages from V$DATAGUARD_STATUS.  
`uuu4[r]`: Archive gaps from V$ARCHIVE_GAP.  
`ww`:      Wait chains (V$WAIT_CHAINS).  

Additionally some report types can contain the letter `i` (idle flag) like
`si` or `eeir` to hide the output of the "idle details". You can use
this flag in the following reports:  
`s`, `tt` - to hide the sessions with the not active status.  
`e`, `ee`, `ss` - to suppress the sessions in the idle wait class event.  
`D`, `II`, `d`, `dd` - to ignore objects without I/O operations.  
`sq` - to filter out sessions with SQL_ID is NULL.  

You can use a "-c" option, Ctrl-C (SIGINT signal) or "kill" command
(SIGTERM signal) to close a database connection properly in reporting mode.  

* `-p` <database password>: If you have specified the database user with a -u option, then you need to specify a password. You can specify it with a -p
option or AMON will ask you for the password during the start.

* `-r` <{sysdba | sysoper | sysasm}>: You can connect to the remote database with an administrative privilege using this option.

* `-s` <{logreads | preads | pwrites | redo | wait_time}>: Use this
option to sort the `s`, `ss`, `ee` reports by the corresponding column.

* `-t[m][r]` <statistic name [,statistic name...]": Use this option, if you look for some specific statistics from V$SYSSTAT or V$SESSTAT views (reporting mode only). Any statistic name can contain the following modifiers (separated by "/"):  
`s` - Statistic value should be calculated per second.  
`K` - Statistic value should be divided by 1024.  
`M` - Statistic value should be divided by 1024*1024.  
`G` - Statistic value should be divided by 1024*1024*1024.  
`k` - Statistic value should be divided by 1000.  
`m` - Statistic value should be divided by 1000000.  
`g` - Statistic value should be divided by 1000000000.  

Additionally you can specify the option "-tr" instead of "-t" to get
the specified statistics for all RAC instances. You should use the "-t"
option together with "-S" or "-P" options, if you look for statistics
from V$SESSTAT for a specific session.

In a multitenant container database you have to add the letter "m" to
this option to get the specified statistics from the V$CON_SYSSTAT view
instead of the default V$SYSSTAT view.

You can specify the keyword "baseline" as the statistic name. This
means, that the following recommended load-related statistics according to
the "Oracle Database Performance Tuning Guide" book will be collected:  

*redo size*  
*session logical reads*  
*db block changes*  
*physical reads*  
*physical read total bytes*  
*physical writes*  
*physical write total bytes*  
*parse count (total)*  
*parse count (hard)*  
*user calls*  
*execute count*  
*DB time*  
*CPU used by this session*  
*parse time elapsed*  
*bytes sent via SQL\*Net to client*  
*bytes received via SQL\*Net from client*  
*SQL\*Net roundtrips to/from client*  
*bytes sent via SQL\*Net to dblink*  
*bytes received via SQL\*Net from dblink*  
*SQL\*Net roundtrips to/from dblink*  


Sometimes you don't know exactly a statistic name. In this case you can
specify a name pattern for "-t" option. This pattern must contain the
"%" character. AMON will use this statistic name as LIKE predicate to
select and output corresponding statistic names.

* `-u` <database user>: Per default AMON tries to connect to the database as a SYS user using the external authentication (dba UNIX group). With the -u
option you can specify any other users with the DBA role.

* `-v`: Print AMON version number and exit.

* `-w` <AMON start window>: You can specify the start window using the same letters as in the AMON help window (interactive mode only). The default start window is "g" (general information window). The available windows for a database instance are:  
`B`   - Automatic big table caching objects (V$BT_SCAN_OBJ_TEMPS).  
`BB`  - Buffer cache details (V$BH).  
`D`   - Database files I/O statistics (V$IOSTAT_FILE).  
`E`   - System wait events statistics (V$SYSTEM_EVENT).  
`EE`  - System wait event classes statistics (V$SYSTEM_WAIT_CLASS).  
`EEE` - CDB System wait event statistics (V$CON_SYSTEM_EVENT).  
`I`   - Instance I/O statistics (V$SYSSTAT).  
`II`  - Instance I/O functions (V$IOSTAT_FUNCTION).  
`L`   - Currently running long operations (V$SESSION_LONGOPS).  
`LL`  - Library cache details (V$DB_OBJECT_CACHE).  
`M`   - Mutex statistics (V$MUTEX_SLEEP).  
`MM`  - Mutex statistics (V$MUTEX_SLEEP_HISTORY).  
`P`   - Process memory details (V$PROCESS).  
`R`  - RMAN jobs status (V$RMAN_STATUS).  
`RR` - RMAN jobs output (V$RMAN_OUTPUT).  
`S`   - SGA statistics (V$LIBRARY_CACHE).  
`T`   - Temporary segment usage (V$TEMPSEG_USAGE).  
`TT`  - Active transactions (V$TRANSACTION).  
`U`   - Redo dest. histograms (V$REDO_DEST_RESP_HISTOGRAM).  
`UU`  - Redo apply histograms (V$STANDBY_EVENT_HISTOGRAM).  
`a`   - ASH details (V$ACTIVE_SESSION_HISTORY).  
`aa`  - Archived redo logs (V$ARCHIVED_LOG).  
`d`   - Datafiles statistics (V$FILESTAT).  
`dd`  - Tempfiles statistics (V$TEMPSTAT).  
`e`   - Grouped wait events (V$SESSION_WAIT).  
`ee`  - Sessions by wait events (V$SESSION_WAIT).  
`g`   - General database information (V$DATABASE, DBA_REGISTRY).  
`gg`  - General CDB details (V$PDBS).  
`h`   - AMON keys (alphabetically).  
`hh`  - AMON keys by usage.  
`l`   - Blocked sessions (V$SESSION_BLOCKERS).  
`ll`  - Locking details (V$LOCK).  
`lll` - Latch statistics (V$LATCH).  
`m`   - Instance memory overview.  
`mm`  - In-memory column store statistics (V$IM_SEGMENTS).  
`n`   - Network statistics (V$SYSSTAT).  
`p`   - Parallel execution details (V$PX_SESSION).  
`pp`  - Auto parallel degree policy details (V$RSRC_CONSUMER_GROUP).  
`r`   - RAC statistics (V$SYSSTAT, V$INSTANCE_CACHE_TRANSFER).  
`rr`   - Recovery details (V$RECOVERY_PROGRESS).  
`rrr`  - Recovery processes (V$RECOVERY_SLAVE).  
`s`   - Session statistics I (V$SESSION).  
`ss`  - Session statistics II (V$SESSION).  
`t`   - System time model statistics (V$SYS_TIME_MODEL).  
`tt`  - Session time model statistics  (V$SESS_TIME_MODEL.  
`ttt` - CDB System time model statistics (V$CON_SYS_TIME_MODEL).  
`u`   - Data Guard overview (V$DATABASE).  
`uu`  - Archiving destinations (V$ARCHIVE_DEST).  
`uuu` - Data Guard details (V$MANAGED_STANDBY).  
`x`   - Exadata statistics (V$SYSSTAT).  

The available windows for a ASM instance are:  
`D`  - ASM clients I/O statistics (V$ASM_DISK_IOSTAT).  
`E`  - System wait events statistics (V$SYSTEM_EVENT).  
`EE` - System wait event classes statistics (V$SYSTEM_WAIT_CLASS).  
`L`  - Running long operations (V$ASM_OPERATION).  
`a`  - ASH details (V$ACTIVE_SESSION_HISTORY).  
`d`  - ASM disks statistics (V$ASM_DISK_STAT).  
`e`  - Grouped wait events (V$SESSION_WAIT).  
`ee` - Sessions by wait events (V$SESSION_WAIT).  
`g`  - General ASM information.  
`h`  - AMON keys (alphabetically).  
`hh` - AMON keys by usage.  
`m`  - Instance memory overview.  

* `--pdb` <PDB_Name>: If you specify the PDB name, the AMON will set this container at the beginning using the following statement:  
  `ALTER SESSION SET CONTAINER=PDB_Name`  

## EXAMPLES

Interactive mode:

`amon`  
Start AMON and connect to the local instance on the current node as a SYS user.  

`amon -u sys -p oracle -d SCAN/Service -r sysdba`  
Start AMON with specified connect details using Easy Connect.  

`amon -S 52`  
Start AMON using dynamic session view for the session with SID 52.  

Reporting mode:

`amon -o s`  
AMON connects as a SYS user and outputs the session details.  

`amon -o sqr -i 30  `
AMON outputs session SQL details for all RAC instances all 30 seconds.  

Help mode:   

`amon -h [ help ]` <== Show help text.  
`amon -h options`  <== Print all AMON options.  
`amon -h -Opt`  <== Show usage of "-Opt" option.  
`amon -h intro` <== Introduction to AMON.  
`amon -h all`   <== Show long AMON documentation.  

## AUTHOR

Andrej Simon <andrej.simon@oracle.com>

## SEE ALSO

amon-intro(7) amon-filter(7) amon-grafana(7)

[Free performance monitoring tool AMON](http://sites.google.com/site/freetoolamon)
