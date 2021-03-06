---
title: Replicate data into Azure Database for MySQL.
description: This article describes data-in replication for Azure Database for MySQL.
services: mysql
author: ajlam
ms.author: andrela
manager: kfile
editor: jasonwhowell
ms.service: mysql
ms.topic: article
ms.date: 06/20/2018
---

# Replicate data into Azure Database for MySQL

Data-in Replication allows you to synchronize data from a MySQL server running on-premises, in virtual machines, or database services hosted by other cloud providers into the Azure Database for MySQL service. Data-in Replication is based on the binary log (binlog) file position-based replication native to MySQL. To learn more about binlog replication, see the [MySQL binlog replication overview](https://dev.mysql.com/doc/refman/5.7/en/binlog-replication-configuration-overview.html). 

## When to use Data-in Replication
The main scenarios to consider using Data-in Replication are:

- **Hybrid Data Synchronization:** With Data-in Replication, you can keep data synchronized between your on-premises servers and Azure Database for MySQL. This synchronization is useful for creating hybrid applications. This method is appealing when you have an existing local database server, but want to move the data to a region closer to end users.
- **Multi-Cloud Synchronization:** For complex cloud solutions, use Data-in Replication to synchronize data between Azure Database for MySQL and different cloud providers, including virtual machines and database services hosted in those clouds.

## Limitations and considerations

### Data not replicated
The [*mysql system database*](https://dev.mysql.com/doc/refman/5.7/en/system-database.html) on the primary server is not replicated. Changes to accounts and permissions on the primary server are not replicated. If you create an account on the primary server and this account needs to access the replica server, then manually create the same account on the replica server side. To understand what tables are contained in the system database, see the [MySQL manual](https://dev.mysql.com/doc/refman/5.7/en/system-database.html).

### Requirements
- The primary server version must be at least MySQL version 5.6. 
- The primary and replica server versions must be the same. For example, both must be MySQL version 5.6 or both must be MySQL version 5.7.
- Each table must have a primary key.
- Primary server should use the MySQL InnoDB engine.
- User must have permissions to configure binary logging and create new users on the primary server.

### Other
- Global transaction identifiers (GTID) are not supported.

## Next steps
- Learn how to [set up data-in replication](howto-data-in-replication.md)
