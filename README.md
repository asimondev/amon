# Free Oracle Performance Tool AMON

This is a main page of *AMON*, the free interactive tool for performance monitoring of Oracle databases.

The tool is written completely in C using Oracle OCI API and UNIX Curses library. 
This allows *AMON* to run on every UNIX terminal. After downloading the tool, you can 
immediately start to use it, if the environment variables (**ORACLE_HOME**, **PATH**, 
**LD_LIBRARY_PATH**, **ORACLE_SID** etc) are set correctly.

**If SQL*Plus can run, then AMON should execute as well.**

The tool executes only **SELECT** statements, so that you can easily test it on any database.

Why shall I use this tool additionally to OEM, SQL Developer etc? The answers could be:

* Sometimes you have got only a UNIX terminal (like a PuTTY window). This could be a case, 
if only the SSH port is allowed or if you work over VPN connection.
* You are comfortable with the Oracle dynamic views. You could of course just use SQL*Plus. 
But it's easier to monitor the changing information with *AMON*, because the tool 
already calculates the delta values and refreshes the window automatically.
* You are already using a UNIX terminal for your work. If you want to check some information, 
it's faster to use AMON and check, for instance, a hanging session or the wait events instead 
of starting a GUI or a browser.

Starting with *AMON* version 2 only the Linux executable files will be provided. At the moment 
the version 2 supports Oracle Release 19c on:
* Oracle Linux 7.
* Ubuntu 22.04 LTS using Oracle Instant Client for Linux x86-64.

Further *AMON* documentation:
* [AMON Reference](https://github.com/asimondev/amon/blob/master/docs/amon.md)
* [AMON on Ubuntu](https://github.com/asimondev/amon/blob/master/docs/amon_ubuntu.md)
* [Introduction to AMON](https://github.com/asimondev/amon/blob/master/docs/amon_intro.md)
* [AMON Filter Option](https://github.com/asimondev/amon/blob/master/docs/amon_filter.md)


***

This tool is developed by *Andrej Simon*, Oracle ACS Germany in my free time. If you have any 
questions or comments, please contact me directly (*andrej.simon@oracle.com*).

***

**Freeware disclaimer**: The author, Andrej Simon, of this freeware accepts no responsibility for 
damages resulting from the use of this product and makes no warranty or representation, 
either express or implied, including but not limited to, any implied warranty of merchantability 
or fitness for a particular purpose. This software is provided "AS IS", and you, its user, 
assume all risks when using it.