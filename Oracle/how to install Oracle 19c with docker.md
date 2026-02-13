# pull the docker image
docker pull swr.cn-north-4.myhuaweicloud.com/ddn-k8s/docker.io/doctorkirk/oracle-19c:latest

## 官方仓库（包含具体命令以及参数配置）
https://hub.docker.com/r/doctorkirk/oracle-19c

## 国内镜像仓库
https://docker.aityp.com/image/docker.io/doctorkirk/oracle-19c:latest

# run the container
Create local directory

`mkdir -p /your/custom/path/oracle-19c/oradata`

`cd /your/custom/path/`

`sudo chown -R 54321:54321 oracle-19c/`

Run the Container

docker run -d --name oracle-19c \
-p 1521:1521 \
-e ORACLE_SID=ORCL \
-e ORACLE_PWD=123456 \
-e ORACLE_CHARACTERSET=AL32UTF8 \
-v /your/custom/path/oracle-19c/oradata/:/opt/oracle/oradata \
swr.cn-north-4.myhuaweicloud.com/ddn-k8s/docker.io/doctorkirk/oracle-19c

# start/stop the container
docker start oracle-19c
docker stop oracle-19c

日志输出如下：（其中46%左右会卡住很久）
```
[root@k8s-master path]# docker run -d --name oracle-19c \
> -p 1521:1521 \
> -e ORACLE_SID=ORCL \
> -e ORACLE_PWD=123456 \
> -e ORACLE_CHARACTERSET=AL32UTF8 \
> -v /your/custom/path/oracle-19c/oradata/:/opt/oracle/oradata \
> swr.cn-north-4.myhuaweicloud.com/ddn-k8s/docker.io/doctorkirk/oracle-19c
ORACLE PASSWORD FOR SYS, SYSTEM AND PDBADMIN: 123456

LSNRCTL for Linux: Version 19.0.0.0.0 - Production on 10-FEB-2026 15:15:18

Copyright (c) 1991, 2020, Oracle.  All rights reserved.

Starting /opt/oracle/product/19c/dbhome_1/bin/tnslsnr: please wait...

TNSLSNR for Linux: Version 19.0.0.0.0 - Production
System parameter file is /opt/oracle/product/19c/dbhome_1/network/admin/listener.ora
Log messages written to /opt/oracle/diag/tnslsnr/1c49eefab7f7/listener/alert/log.xml
Listening on: (DESCRIPTION=(ADDRESS=(PROTOCOL=ipc)(KEY=EXTPROC1)))
Listening on: (DESCRIPTION=(ADDRESS=(PROTOCOL=tcp)(HOST=0.0.0.0)(PORT=1521)))

Connecting to (DESCRIPTION=(ADDRESS=(PROTOCOL=IPC)(KEY=EXTPROC1)))
STATUS of the LISTENER
------------------------
Alias                     LISTENER
Version                   TNSLSNR for Linux: Version 19.0.0.0.0 - Production
Start Date                10-FEB-2026 15:15:18
Uptime                    0 days 0 hr. 0 min. 0 sec
Trace Level               off
Security                  ON: Local OS Authentication
SNMP                      OFF
Listener Parameter File   /opt/oracle/product/19c/dbhome_1/network/admin/listener.ora
Listener Log File         /opt/oracle/diag/tnslsnr/1c49eefab7f7/listener/alert/log.xml
Listening Endpoints Summary...
  (DESCRIPTION=(ADDRESS=(PROTOCOL=ipc)(KEY=EXTPROC1)))
  (DESCRIPTION=(ADDRESS=(PROTOCOL=tcp)(HOST=0.0.0.0)(PORT=1521)))
The listener supports no services
The command completed successfully
[WARNING] [DBT-06208] The 'SYS' password entered does not conform to the Oracle recommended standards.
   CAUSE:
a. Oracle recommends that the password entered should be at least 8 characters in length, contain at least 1 uppercase character, 1 lower case character and 1 digit [0-9].
b.The password entered is a keyword that Oracle does not recommend to be used as password
   ACTION: Specify a strong password. If required refer Oracle documentation for guidelines.
[WARNING] [DBT-06208] The 'SYSTEM' password entered does not conform to the Oracle recommended standards.
   CAUSE:
a. Oracle recommends that the password entered should be at least 8 characters in length, contain at least 1 uppercase character, 1 lower case character and 1 digit [0-9].
b.The password entered is a keyword that Oracle does not recommend to be used as password
   ACTION: Specify a strong password. If required refer Oracle documentation for guidelines.
Prepare for db operation
10% complete
Copying database files
40% complete
Creating and starting Oracle instance
42% complete
46% complete

50% complete
54% complete
60% complete
Completing Database Creation
66% complete
```