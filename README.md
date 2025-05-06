select current_user; ----------->>> It will show current user
\l   ----------->>>> It will show list of databases
create database postgresdb   ------------>>>> It will create the databases
\c (database name)  -------------->>>>>>> It will connect to other database
\dn   ------------>>>> It will show List of schema (Default schema is PUBLIC)
\dt ----------->>>> It will show List of tables (relations)
\du  --------->>>>> Tofind the super user
\dt schema.*  -------->>>>> It will show the list of tables under schema.
\d tablename  ---->>>> It will show the table strucuture.
select obj_discription('public.employee'::regclass);  ---->>>> To see the table level comments is there or not in table.
show data_directory;  ----->>>> It will show the data directory path
show port; ----->>>> It will show the port
===================================================================================================================
Virtual mechnie Installation:


===================================================================================================================
Linux Installation:
-------------------
Goto -> settings -> system -> pointing device = USB Multi-touch tablet
Goto -> settings -> storage -> contoller IDLE -> cliick on plus simble -> select the opreatiing system 
Goto -> settings -> Network -> Enable Network Adaptor -> Bride Adaptor (Default -> NAT)

===================================================================================================================
postgresql installation prereqsites
====================================
rpm -qa gcc
make -version

======================
Optional Prereqsitestable stu
======================
rpm -qa readline
rpm -qa zlib

=======================
wget https://ftp.postgresql.org/pub/source/v15.10/postgresql-15.10.tar.gz    -------->>>> direct download the software in server
===========================================================================
Postgresql software installation
--------------------------------
1. Need to copy the software from Local to server
2. tar -xvzf postgresql-15.10.tar.gz
3.  ./configure --without-readline --without-zlib   ---->>>> It's going to verify the prerequisites for postgres software installation
4. make  (It will convert from C language to sql language)
5. make install (It's going to install defualt location) ------>>>> defualt location (/usr/local/pgsql)

==========================================================================================================
User creation
-------------
useradd postgres
cat /etc/passwd
passwd postgres  ---->>>> To change the password

==========================================================================================================
Create data directory and change the ownership for the data files and config files i.e /u01/data15
---------------------------------------------------------------------------------------------------
1. mkdir -p /u01/data15
2. chown -R postgres:postgres /u01/data15
3. chmod -R 775 /u01/data15

============================================================================================================
Creating  cluster 
-----------------
/usr/local/pgsql/bin/initdb -D /u01/data15/     ------->>>> craeting data directory cluster
/usr/local/pgsql/bin/pg_ctl -D /u01/data15/ -l logfile start  ------->>>> start the cluster directory
/usr/local/pgsql/bin/psql    --------->>>>> Start the postgres database

==============================================================================================================
Custom installation of postgres
--------------------------------
mkdir -p /u01/app/pg15/pg_home
/u02/data15 (data directory) 

1. ./configure --prefix=/u01/app/pg15/pg_home  (coustomize postgres installation location)
2. make
3. make install

==============================================================================================================
custom - createing cluster
-------------------------
1. /u01/app/pg15/pg_home -D  /u02/data15 -U postgres1  -------->>>> To give the specific user (-U postgres1)
2. Need one user (postgres) at OS level 
3. Need one data direcory (/u02/data15)

==============================================================================================================
connect to postgres database to specific user
---------------------------------------------
/u01/app/pg15/pg_home/bin/psql -d postgres (database name) -U postgres1 (username)  ------>>>> To coonect postgres databse to postgres1 user

==============================================================================================================
Postgressql installation via yum method
===========================================
No need to download the software 
No need to create user at OS level
No need to create data directory and give permissions.
------------------------------------------------------
PostgreSQL Yum Repository
-------------------------
# Install the repository RPM:
sudo yum install -y https://download.postgresql.org/pub/repos/yum/reporpms/EL-7-x86_64/pgdg-redhat-repo-latest.noarch.rpm    ----->>> Saved in this location (cat /etc/yum.repos.d/)

# Install the Postgresql:
sudo yum install -y postgresql15-server

# Optionally initilize the database and enable automatic start:
sudo /usr/pgsql-15/bin/postgresql-15-setup initdb
sudo systemctl enable postgresql-15
sudo systemctl start postgresql-15

cd /usr/pgsql-15/   ------>>>> (defualt installation location)

================================================================================================================================
Customize Postgres installation
-------------------------------
We can not customize installation location.
We can customize data directory location
We can customize super user.

================================================================================================================================
