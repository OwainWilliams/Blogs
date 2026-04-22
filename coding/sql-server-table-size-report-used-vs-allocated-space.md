# SQL Server Table Size Report (Used vs Allocated Space)

##

### **Overview**

This page documents a SQL Server query used to analyse **table‑level storage usage** within a database. It provides a breakdown of how much space each table consumes, both in terms of **used pages** and **allocated pages**, and orders the results from largest to smallest.

This is useful for:

* Capacity planning
* Identifying unusually large tables
* Performance tuning
* Understanding storage growth over time

***

### **Purpose of the Query**

SQL Server stores data in **8 KB pages**, grouped into allocation units. This query aggregates those pages for each table and converts them into megabytes, giving you a clear view of:

* **Used MB** – space actively used by the table
* **Allocated MB** – space reserved by SQL Server for future growth

The result is a concise report showing which tables consume the most space.

***

### **The SQL Query**

```sql
select schema_name(tab.schema_id) + '.' + tab.name as [table],
    cast(sum(spc.used_pages * 8)/1024.00 as numeric(36, 2)) as used_mb,
    cast(sum(spc.total_pages * 8)/1024.00 as numeric(36, 2)) as allocated_mb
from sys.tables tab
    inner join sys.indexes ind 
        on tab.object_id = ind.object_id
    inner join sys.partitions part 
        on ind.object_id = part.object_id and ind.index_id = part.index_id
    inner join sys.allocation_units spc
        on part.partition_id = spc.container_id
group by schema_name(tab.schema_id) + '.' + tab.name
order by sum(spc.used_pages) desc;
```

***

### **How It Works**

#### **1. Table Identification**

`sys.tables` provides the list of all user tables in the database.

#### **2. Joining System Views**

The query joins:

* `sys.indexes` – to include all index structures
* `sys.partitions` – to access partition-level metadata
* `sys.allocation_units` – to retrieve page counts

These views together expose how SQL Server physically stores table data.

#### **3. Calculating Space Usage**

SQL Server pages are 8 KB each.\
The query converts pages → KB → MB:

```
pages * 8 KB / 1024 = MB
```

Two metrics are calculated:

* **used\_pages** → actual data
* **total\_pages** → allocated space

#### **4. Grouping and Ordering**

Tables are grouped by schema and name, then sorted by **largest used space first**.

***

### **Example Output**

| table                | used\_mb | allocated\_mb |
| -------------------- | -------- | ------------- |
| dbo.Orders           | 512.00   | 768.00        |
| sales.TransactionLog | 430.25   | 512.00        |
| dbo.Customers        | 120.50   | 256.00        |

_(Values shown are illustrative.)_

***

### **When to Use This Query**

Use this script when you need to:

* Audit database size
* Identify large or growing tables
* Investigate performance issues related to storage
* Prepare for migrations or archiving
* Monitor space usage trends

***

### **Related Tools & Queries**

* `sp_spaceused` for quick table-level stats
* `sys.dm_db_partition_stats` for row counts
* Index fragmentation reports
* Filegroup and database size queries

***

If you'd like, I can also generate:

* A shorter “quick reference” version
* A version formatted for Confluence, GitHub Wiki, or Azure DevOps Wiki
* A companion page explaining how to automate this report

Just tell me the style you want.



Thanks Jack for sharing this.&#x20;
