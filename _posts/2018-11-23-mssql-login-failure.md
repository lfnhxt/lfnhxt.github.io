---
layout: post
title: MSSQL2008登陆失败
group: MSSQL
---

## MSSQL2008登陆失败,情况如下:
1.Windows身份登陆MSSQL失败，错误:18456   
2.忘记sa密码，无法登陆MSSQL   
   
## 解决办法
1.管理员打开cmd命令   
2.cmd执行net stop mssqlserver   
3.转到mssqlserver安装目录。 例:C:\Program Files\Microsoft SQL Server\MSSQL10_50.MSSQLSERVER\MSSQL\Binn   
4.cmd执行"C:\Program Files\Microsoft SQL Server\MSSQL10_50.MSSQLSERVER\MSSQL\Binn\sqlserver.exe" /m /f   
5.打开Sql Server Managerment Studio.   
6.不要马上连接，先取消，然后左上角点击新建查询，然后连接   
7.执行角本   
```sql
--打开xp_cmdshell功能
EXEC [sys].[sp_configure] @configname = 'xp_cmdshell', -- varchar(35)
    @configvalue = 1 -- int
RECONFIGURE WITH override


--修改注册表，修改身份验证为混合验证方式
USE [master]
GO
EXEC xp_instance_regwrite N'HKEY_LOCAL_MACHINE', N'Software\Microsoft\MSSQLServer\MSSQLServer', N'LoginMode', REG_DWORD, 2
GO

--创建登录名
CREATE LOGIN [计算机名\Administrator] FROM WINDOWS;
GO

--赋予登录名的权限为sysadmin
USE master
GO
EXEC [sys].[sp_addsrvrolemember] @loginame = '计算机名\Administrator', -- sysname
    @rolename = sysadmin -- sysname

--关闭xp_cmdshell功能
EXEC [sys].[sp_configure] @configname = 'xp_cmdshell', -- varchar(35)
    @configvalue = 0 -- int
RECONFIGURE WITH override
```
8.关掉SQLSERVER
9.打开SQLSERVER配置管理器，启动SQLSERVER
10.打开Sql Server Managerment Studio即可通过windows身份登陆.