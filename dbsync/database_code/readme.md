#Process logs in primary for monitoring

##Set ssh key exchange between standby and primary
As usual

##Set dbsync to copy back log files

PRIMARY_HOST=<primary_host>
PRIMARY_LOGFILE_BASE_DIR=<base_log_dir>

##Set up primary to process the logs

First check the update location of logs in CREATE DIRECTORY in create_external_table_dbsync_logs.sql

SQL> @create_external_table_dbsync_logs.sql

SQL> @sys_grants
 
SQL> conn YOUR_DBSYNC_MONITOR_USER

SQL> @primary_db_objects.sql

SQL> @dbsync.pks

SQL> @dbsync.pkb

SQL> @process_logs_job.sql

now check the jobs

SQL> col what format a30

SQL> select what,to_char(next_date,'dd-mon-yyyy hh24:mi:ss') next_date,broken,failures from dba_jobs where schema_user='<dbsync_user>';
