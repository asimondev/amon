# Introduction to AMON

## SYNOPSIS

`amon` [<args>]

### Interactive mode:
   amon -i interval -w window -S sid -P pid -f filter -b {y|n}
     -u user -p password -d database -r {sysdba | sysoper | sysasm}
     --pdb PDB -a directory -A minutes -e {b|t|a} -l {y|n}
     -h -v -D {1|4|8|12|1000}

### Reporting mode:
   amon {-o report type | -O report type | -t[m][r] "name1, name2, .."}
     -i interval -c count -C paging -f filter -S sid -P pid
     -u user -p password -d database -r {sysdba | sysoper | sysasm}
     --pdb PDB -l {y|n} -h -v -D {1|4|8|12|1000}

### Help parameters:
   amon -h [ { help (this text!) | -Opt | options | intro | all } ]

## OPTIONS
  You can find the description of all AMON options in amon(7).


## DESCRIPTION

amon(7) is a free performance monitoring tool for Oracle databases. The
tool is written in C using Oracle OCI API and UNIX Curses library. This allows
AMON to run on every UNIX terminal. After downloading this tool, you can
immediately start to use it. If SQL*Plus can run, then AMON should
execute as well.

AMON executes only SELECT statements, so that you can easily test it on any
database. **No database changes** are made by AMON.

Before starting AMON make sure, that all required environment variables for
ORACLE database are set (ORACLE_HOME, LD_LIBRARY_PATH, PATH). It's recommended
to use local internal connect as SYSDBA user. (ORACLE_SID environment
  variable should be set.)

### Starting AMON in interactive mode:

In interactive mode the AMON is executed similar to the UNIX "top" utility.
You would start the program, see the performance metrics and use the keys to
manage the output. Usually would you set ORACLE_SID and just type in "amon"
to start AMON. The default window shows the general database information.
The second line shows the keys, which are available in this window.

All AMON commands are given with the keyboard. The arrow keys, *Return* keys
etc does not have any function in AMON. So the usage of AMON is similar to the
great "Vi" editor.

You use `q` to leave the AMON and `h` or `hh`to see the mapping between
specific keys and available performance views. By pressing these keys you
can always leave the current window and go to the target window. (No extra
  *Return* key is required.) For instance, the `s` will show you the
  sessions overview. The key combination `ee` will get you to the
  currently waiting sessions from the V$SESSION_WAIT.

Usually you can use the "Vi" keys "j", "k", "f" and "b" to move the cursor
to the next/previous line or page. If you want to see more details for the
specific line, you can usually use `z` to "zoom" in or "zoom" out. On each
window you can see other specific keys for this particular performance
window on the second line.

Some windows provide *Save* command, which can be activated by pressing the `0`
(zero!) key. This command would save the current window content to the
text file.

The default refresh interval is 10 seconds. By pressing `+` or `-` keys you
can double or cut by half the refresh time. Usually the default value of 10
seconds is Ok.

### Starting AMON in reporting mode:

In reporting mode the AMON is executed similar to the UNIX "sar" or "vmstat"
utilities. You would specify the desired performance metrics by using the
`-o` option and start the program. The output will be written to the
terminal. You can use the UNIX tee command to see the standard output and
move the output to a file at the same time.

You can only specify one performance metric in AMON reporting mode. If you
want to monitor two different metrics, you would have to start AMON twice
with the desired options.

## EXAMPLES

Interactive mode:

`amon`  
Start AMON in interactive mode and connect to the local instance on the
current node as a SYS user (like sqlplus / as sysdba).  

`amon -u sys -p oracle -d racscan/mydb.world.com -r sysdba`  
Start AMON with specified connect details using Easy Connect.  

`amon -S 52`  
Start AMON using dynamic session view for the session with SID 52.  

`amon -S 52`  
Start AMON using dynamic session view for the session with SID 52.  

`amon -P 22536`  
Start AMON using dynamic session view for the session with OS process
ID 22536 (SPID column from V$PROCESS view). Use it, for instance, to
monitor a session, which consumes much CPU. In this case you can get
the PID column from the "top" output on the database server.

Reporting mode:

`amon -o s`  
AMON connects as a SYS user and outputs the session details.  

`amon -o sqr -i 30`  
AMON outputs session SQL details for all RAC instances all 30 seconds.  


## AUTHOR

Andrej Simon <andrej.simon@oracle.com>

## SEE ALSO

amon(7) amon-filter(7) amon-grafana(7)

[Free performance monitoring tool AMON](http://sites.google.com/site/freetoolamon)
