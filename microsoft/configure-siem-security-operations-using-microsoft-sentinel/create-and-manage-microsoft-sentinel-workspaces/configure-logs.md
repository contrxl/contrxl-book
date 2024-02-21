---
description: Unit 7.
---

# Configure Logs

Microsoft Sentinel has three primary log types:

* Analytics Logs
* Basic Logs
* Archive Logs

Data in each table is retained for a specified time after which it is removed or archived with a reduced retention fee. To access archived data, it must be retrieved from an Analytics Log table using one of the following methods:

* Search Jobs
* Restore

### Analytical Logs

All tables in a workspace are of the type Analytical Logs by default, these are available to all features of a Log Analytics workspace and any other service that uses the workspace.

### Basic Logs

Certain tables can be configured as Basic Logs to reduce the cost of storing high-volume verbose logs for debugging but not analytics. Tables configured for Basic Logs have reduced features, reduced cost and are only retained for 8 days.

### KQL Language Limits

Queries against Basic Logs are optimised for simple data retrieval using the following operators:

* where
* extend
* project
* project-away
* project-keep
* project-rename
* project-reorder
* parse
* parse-where

The following isn't supported:

* join
* union
* aggregates (summarise)

### Tables Supporting Basic Logs

Currently the following tables can be configured for Basic Logs:

* All tables created with the Data Collection Rule (DCR)-based custom logs API.
* ContainerLogV2, which Container Insights uses and includes verbose text-based log records.
* AppTraces, which contains freeform log records for application traces in Application Insights.

### Configure Log Type

To adjust the log type for an eligible table, select the workspace settings from the Microsoft Sentinel Settings area. The next screen is the Log Analytics portal:

1. Select "Tables" tab.
2. Select the table and then ... at the end of the row.
3. Select Manage table.
4. Change the Table Plan.
5. Select Save.

### Configure Table Retention

1. Select "Tables" tab.
2. Select the table and then ... at the end of the row.
3. Select Manage table.
4. Change the Total Retention Period.
5. Select Save.
