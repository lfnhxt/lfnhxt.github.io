---
layout: post
title: Install SMO
group: Microsoft Visual Studio
---

## 为什么安装SMO
项目出现了以下错误   
命名空间"Microsoft.SqlServer"中不存在类型或命名空间名"Management"(是否缺少程序集引用?)   
   
未能找到引用的组件"Microsoft.SqlServer.ConnectionInfo"   
未能找到引用的组件"Microsoft.SqlServer.Management.Sdk.Sfc"   
未能找到引用的组件"Microsoft.SqlServer.Smo"   
未能找到引用的组件"Microsoft.SqlServer.SqlEnum"   
   
## [安装SMO](https://docs.microsoft.com/en-us/sql/relational-databases/server-management-objects-smo/installing-smo?view=sql-server-2017)
* 1.[使用NuGet 包管理器 UI](https://docs.microsoft.com/zh-cn/nuget/tools/package-manager-ui#install-options)
* 2.查找并安装Microsoft.SqlServer.SqlManagementObjects