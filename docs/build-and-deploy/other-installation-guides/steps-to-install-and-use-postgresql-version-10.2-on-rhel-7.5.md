# Steps to Install and use PostgreSql Version 10.2 on RHEL 7.5

Often simply Postgres, is an object-relational database management system \(ORDBMS\) with an emphasis on extensibility and standards compliance. It can handle workloads ranging from small single-machine applications to large Internet-facing applications \(or for data warehousing\) with many concurrent users Postgresql Prerequisites On a Linux or Mac system, you must have superuser privileges to perform a PostgreSQL installation. To perform an installation on a Windows system, you must have administrator privileges.

## Steps to install Postgresql in RHEL-7.5

### Download and install PostgreSQL.

```text
    $ sudo yum install https://download.postgresql.org/pub/repos/yum/10/redhat/rhel-7-x86_64/pgdg-redhat10-10-2.noarch.rpm 
    $ sudo  yum-config-manager --disable pgdg95
```

### Check the postgresql packages

```text
    $ sudo yum update 
    $ sudo yum list postgresql*
```

### Installation command

```text
    $ sudo yum install postgresql10 postgresql10-server
    $ sudo /usr/pgsql-10/bin/postgresql-10-setup initdb
    $ sudo systemctl enable postgresql-10
```

### Postgresql service stop/start/restart command

```text
    $ sudo systemctl start postgresql-10
    $ sudo systemctl status postgresql-10 
    $ sudo systemctl stop postgresql-10
```

To changing default port 5432 to 9001 and connection + buffer size we need to edit the postgresql.conf file from below path PostgreSQL is running on default port 5432. you decide to change the default port, please ensure that your new port number does not conflict with any services running on that port.

## Steps to change the default port

### Open the file  and modify the below changes

```text
    $ sudo vi /var/lib/pgsql/10/data/postgresql.conf
```

```text
listen_addresses = '*'   (changed to * instead of local host )
port = 9001       ( uncomment port=5432 and change the port number 
Open the port 9001 from the VM 
```

### Use below command to open the port 9001 from RHEL 7.5 VM

```text
    $ sudo firewall-cmd --zone=public --add-port=9001/tcp --permanent
    $ sudo firewall-cmd --reload
```

### To increase the buffer size and number of postgreSql connection same fine modify the below changes also

```text
    $ sudo vi /var/lib/pgsql/10/data/postgresql.conf 

    unix_socket_directories = '/var/run/postgresql, /tmp' max_connections = 1000
    shared_buffers = 2GB
```

### Start the service

```text
    $ sudo systemctl start postgresql-10
```

### To change the default password

#### Login to postgrsql

```text
    $ sudo su postgres
    bash-4.2$ psql -p 9001
    postgres=# \password postgres
    Enter new password:
    Enter it again:
    postgres=# \q
```

#### Restart the service:

```text
    $ sudo systemctl restart postgresql-10
```

It will ask new password to login to postgresql

**Example for sourcing the sql file form command line**

```text
    $ psql --username=postgres --host=<server ip> --port=9001 --dbname=postgres
```

### Open the file

```text
    $ sudo vim /var/lib/pgsql/10/data/pg_hba.conf
```

 **Default lines are present in `pg_hab.conf` file**

| TYPE | DATABASE | USER | ADDRESS | METHOD |
| :--- | :--- | :--- | :--- | :--- |
| local | all | all |  | peer |
| host | all | all | 127.0.0.1/32 | ident |
| host | all | all | ::1/128 | ident |
| local | replication | all |  | peer |
| host | replication | all | 127.0.0.1/32 | ident |
| host | replication | all | ::1/128 | ident |

 **Modify with below changes in file `/var/lib/pgsql/10/data/pg_hba.conf`**

| TYPE | DATABASE | USER | ADDRESS | METHOD |
| :--- | :--- | :--- | :--- | :--- |
| local | all | all |  | md5 |
| host | all | all | 127.0.0.1/32 | ident   |
| host | all | all | 0.0.0.0/0 | md5   |
| host | all | all | ::1/128 | ident   |
| local | replication | all |  | peer   |
| host | replication | all | 127.0.0.1/32 | ident   |
| host | replication | all | ::1/128 | ident   |

```text
$ sudo systemctl status postgresql-10
```

**Reference link:** [https://www.tecmint.com/install-postgresql-on-centos-rhel-fedora](https://www.tecmint.com/install-postgresql-on-centos-rhel-fedora)

