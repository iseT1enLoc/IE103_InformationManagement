# IE103-INFORMATION MANAGEMENT

This repository is intended to **_give a summarize notes_** of what i have learned and implement data replication in PostgreSQL. PostgreSQL WAL mechanism for further use.

# 1-Set up and using docker

To successfully simulate this data replication project, I highly appreciate the enthusiastic guilde from Marcel Dempers [Github](https://github.com/marcel-dempers/docker-development-youtube-series/tree/master/storage/databases/postgresql)

In this repository, he will work us through the most basic tasks from docker setup and higher complex tasks such as change the config files in postgresql.

## 2-WAL-writing ahead log.

<img src=".\media\WAL.png" width="200" height="150" alt="Cat picture">
!["WAL"](.\media\WAL.png "WAL mechanism")
This is a mechanism that help to recover whenever our database crashes.

Suppose we have a backup version on **Monday** but the database crash on the following **Saturday**.

We do not have the backup version between the interval from tuesday to saturday, the WAL file will help us do this things.

# 3-Some important configs file in PostgreSQL.

In Window version, we can find the configs find in **‘.\PostgreSQL\16\data\{intended file}’** path.

## 2.1.pg_hba.conf

**pg_hba.conf** stands for host-based authentication file. It is like the postgres firewall configuration. It tell us which ip address or which user we can trust.

## 2.2.pg_ident.conf

This allow us to map operating system user account to database user.

## 2.3.postgresql.conf

This is one of the critical configuration file that we should look into.

There is a hundreds line of document writing about this file but in this section we will focus on only a few parts.

- **File location:**
  - We can manually direct where the data is stored by setting parameter **data =”**path to location**”.**
  - Parameters**-hba_file** :This line points to the configuration file that controls how clients can connect to the PostgreSQL server. It defines which users or IP addresses are allowed to connect, and what authentication method they must use (e.g., password, MD5). This file is crucial for securing your database server.
  - Parameters-**ident_file:** it point to the customer pg_ident.conf file.
- **Connection and Authentication**
  This part include sections:
  - Connection settings: we can config information suchas max-connections, suitable port number (5432 by default).
  - TCP settings: tcp_keepalives_idle, tcp_keepalives_interval, tcp_keepalives_count, tcp_user_timeout.
  - Authentication settings: the easiest information of this part is **password_encryption** technique, we can choose from various technique such as scram-sha-256, md5 and so on.
  -
