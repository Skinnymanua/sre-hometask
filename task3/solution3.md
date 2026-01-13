# Based on the fired alert, it should monitor MySQL replica health

## Alert breakdown:
```
- alert: ReplicationNotRunning"
```
### Alert name
```
expr: 

```
### Displays metrics used for the alert rule
```
mysql_slave_status_slave_io_running 
```
### metric monitors replication I/O thread
```
mysql_slave_status_slave_sql_running
```
### metric monitors replication SQL thread
```
== 0 
```
### equals not running thread

### 'or' operator between them means the alert fires when one of the threads aren't running

```
for: 2m
```
### According to prometheus documentation, the optional 'for" clause causes Prometheus to wait for a certain duration between first encountering a new expression output vector element and counting an alert as firing for this element. In this case, Prometheus will check that the alert continues to be active during each evaluation for 10 minutes before firing the alert. Elements that are active, but not firing yet, are in the pending state. 

### This may prevent false-positive alerts during restarts or temporary connectivity issues.

```
.labels.severity: warning
```
### Alert criticality level
```
description: 'Slave replication (IO or SQL) has been down for more than 2 minutes on pod:`{{ $labels.pod }}`'
```
### Brief description of the issue; `{{ $labels.pod }}` displays which exact pod experiencing an issue

## Possible reasons why the alert may fire
### - Primary MySQL down or unreachable
### - Wrong replication credentials
### - Disk full on replica
### - Duplicate key / SQL error
### - Network issue between pods
### - Replica restarted and not reconfigured

## Fixing

### Investigate the issue by accessing the mysql pod via ssh, then logging in to mysql and requesting the slave status:
```
kubectl exec -it pod/mysql --bash

mysql -u root -p

mysql: # SHOW SLAVE STATUS \G
```
### Depending on the output fixes may vary from simple restart to resolving replication issues (e.g. duplicate keys)
