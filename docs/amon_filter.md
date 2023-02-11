# AMON Filter Option

## SYNOPSIS

`amon` [<-f FilterName:FilterValue>]

## DESCRIPTION

You can use AMON filter option in both interactive and reporting mode. The
filter condition will be applied to the result set before displaying.

The filter name is not case sensitive. But the filter value is case sensitive
and will be used as LIKE expression in the WHERE clause of the
following interactive windows and reports:  

- `ASH view and reports.`  
- `Session views and reports.`  
- `Wait events views and reports.`  
- `Time model statistics views and reports.`  
- `Process memory details view and report.`  

If you provide many filters, they will be merged with AND expression. This is
the default mode. You could also specify "+" (for OR) or "-" (for NOT) for
the second and other filters.

## OPTIONS
  The possible filter names are:  

- `CLIENT_INFO:`<string>: The CLIENT_INFO string.
- `COMMAND:`<string>: SQL command from V$SQLCOMMAND. This filter is used only for sessions.
- `CON_ID:`<number>: Container ID for a CDB database.
- `CON_NAME:`<string>: Container name for a CDB database.
- `EVENT:`<string>: Wait event name.
- `INST_ID:`<number>: Instance ID. This filter applies only in RAC mode.
- `INST_NAME:`<string>: Instance name. This filter applies only in RAC mode.
- `MACHINE:`:<string>: Client host name.
- `MODULE:`<string>: Module name.
- `OSUSER:`:<string>: Client OS user.
- `PROGRAM:`<string>: Client program name.
- `SERVICE:`<string>: Database service name.
- `SQL_ID:`<string>: Statement SQL_ID.
- `SQL_MON:`<YES>: The only possible values is YES. AMON will selects only sessions with
  entries in the V$SQL_MONITOR view.
- `SQL_TEXT:`<string>: SQL statement. This filter is only available in reporting mode (`-o sq`).
- `USER:`<string>: Database user.

## EXAMPLES   

### USER Filter
`amon -f "USER:SYS"`  

AMON will start in interactive mode and will limit the sessions in the corresponding windows to the SYS user 
sessions only. Usually would like to see the SYS user sessions, so you could start AMON with this filter and
go to the session view (*s*) immediately:

`amon -f "user:SYS" -w s`

### PROGRAM Filter

Sometimes you would like check the sessions started with specific program. For instance, you can use this 
command to check for the SQL*Plus session:

`amon -f "program:sqlplus%" -w s`

### Advanced Filters

`amon -o s -f "-service:%BACKGROUND%" -f "program:sqlplus%" -f "+-program:amon%"`  

Get AMON sessions report without background services. The sessions with
sqlplus program will be included. Sessions with amon program will be
exluded. Here is the output from the corresponding SELECT statement in AMON:

`AND (a.service_name NOT LIKE '%BACKGROUND%' AND  ( a.program LIKE 'sqlplus%' OR a.program NOT LIKE 'amon%' ))`

## AUTHOR

Andrej Simon (*andrej.simon@oracle.com*)

## SEE ALSO

* [AMON Reference](https://github.com/asimondev/amon/blob/master/docs/amon.md)
* [Introduction to AMON](https://github.com/asimondev/amon/blob/master/docs/amon_intro.md)
* [AMON on Ubuntu](https://github.com/asimondev/amon/blob/master/docs/amon_ubuntu.md)
