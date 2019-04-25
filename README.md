# taTaskSchedule
## 调度测试工具
- 1、模拟流程单节点调度测试，可同时调度主库、分库并发、UFT并发调度等
- 2、可模拟任意流程节点调度，查看相应的调度日志信息
- 3、支持mysql和oracle数据库，方便前后台开发人员本地调度测试

## 配置说明
- 1、把工具下载拷贝到本地
- 2、配置taconf目录下的后台t2连接配置和本地bpme数据库连接
## application.properties
- 1、指定本地测试数据库类型
```
#数据库类型
dbtype=org.hibernate.dialect.MySQL5Dialect
#dbtype=org.hibernate.dialect.Oracle10gDialect
```
## t2sdk-config.xml
- 1、替换配置中对应的后台连接地址和端口
```
<?xml version="1.0" encoding="UTF-8"?>
<t2sdk-configuration>
  <performance debug="true" localServerName="t2sdkll" reconnInterval="10" callBackTime="10000" heartbeatTime="2000" sendPoolSize="10" senderQueueLength="40" />
  <parents>
    <parent safeLevel="NONE" parentName="business">
      <limit licenseFile="taconf/client_license.dat" encrypt="blowfish" />
      <members>
        <member address="192.168.37.162" port="8999" no="0" poolSize="1" />
      </members>
    </parent>

  </parents>
</t2sdk-configuration>
```
## resources.properties
- 1、配置本地流程引擎数据库，方便配置后台调度节点和查看调度日志
- 2、配置要测试的流程调度节点和想测试输入的调度参数信息
```
# mysql数据库连接配置
resource.ds1.className=bitronix.tm.resource.jdbc.lrc.LrcXADataSource
resource.ds1.uniqueName=jdbc/bpme
resource.ds1.minPoolSize=100
resource.ds1.maxPoolSize=300
resource.ds1.driverProperties.driverClassName=com.mysql.jdbc.Driver
resource.ds1.driverProperties.url=jdbc:mysql://localhost:3306/bpme_uft?useUnicode=true&amp;characterEncoding=UTF-8
resource.ds1.driverProperties.user=root
resource.ds1.driverProperties.password=root
resource.ds1.allowLocalTransactions=true
resource.ds1.enableJdbc4ConnectionTest=true
resource.ds1.testQuery=select now()

# oracle数据库连接配置
# resource.ds1.className=oracle.jdbc.xa.client.OracleXADataSource
# resource.ds1.uniqueName=jdbc/bpme
# resource.ds1.minPoolSize=10
# resource.ds1.maxPoolSize=50
# resource.ds1.driverProperties.URL=jdbc:oracle:thin:@10.20.27.136:1521:ora11g
# resource.ds1.driverProperties.user=bpme_l
# resource.ds1.driverProperties.password=bpme_l
# resource.ds1.allowLocalTransactions=true
# resource.ds1.enableJdbc4ConnectionTest=true

# 调度执行节点
taskCode=ReqDeal_1

# 调度执行数据 
executeData = {"c_instanceid" : "20100513F6100001","c_tenantid" : "*","c_longtacode" : "F6","c_liqbatchno" : "1","l_shardingno" : "0"}



```
## execute.bat
配置信息完成后，执行execute.bat开始调度测试

## 问题反馈
有问题可直接联系作者反馈
