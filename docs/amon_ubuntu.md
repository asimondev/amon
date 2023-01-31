# Using AMON on Ubuntu 22.04 LTS.

## Installing Oracle Instant Client and AMON.

Before using AMON on Ubuntu, you have to install Oracle Instant Client for Linux x86-64. 
You can download the corresponding files from 
[Oracle Instant Client Downloads for Linux x86-64](https://www.oracle.com/de/database/technologies/instant-client/linux-x86-64-downloads.html).

You need Oracle 19c Instant Client 64b-bit Basic Package, for instance, 19.17 to run AMON. After 
downloading the Instant Client zip file, you should unzip it in a new directory. AMON 
file should be also unzipped in any other directory. After setting the environment variables
you can start AMON and connect to your remote database using Easy Connect descriptor and 
your account with SYSDBA role. (The SYSDBA role is recommended to get access to all dynamic views.)

## Example of installing and starting AMON using Instant Client.

The AMON and Instant Client Basic Package were already uploaded to the *~/tmp* directory.

Create new directories below the *$HOME* directory (*/home/andrej*) and unpack the files.

```
cd $HOME
mkdir bin instant_client
cd ~/instant_client
unzip ~/tmp/instantclient-basic-linux.x64-19.17.0.0.0dbru.zip
cd ~/bin
cp ../tmp/amon_19c_ubuntu_22.04.gz .
gunzip ./amon_19c_ubuntu_22.04.gz 
```

Usually you would add the following lines to your Bash profile. But you can also 
execute them on it's own before starting AMON.

```
export AMON_INSTANT_CLIENT=/home/andrej/instant_client/instantclient_19_17
export LD_LIBRARY_PATH=$AMON_INSTANT_CLIENT:$LD_LIBRARY_PATH
export PATH=/home/andrej/bin:$PATH
```

Now you can use your SYS account and Easy Connect descriptor to run AMON:  
`amon_19c_ubuntu_22.04 -u sys -d rkol7dev1/a19a -r sysdba `

You would connect as a database user SYS with the role SYSDBA. The database with 
the service name *a19a* runs on the host *rkol7dev1* using the default listener 
port *1521*. AMON will ask you for the SYS password. If you like you can use the 
*-p* option and specify the password directly on the command line.
