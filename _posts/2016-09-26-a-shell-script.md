---
layout: post
title: "一个查询数据库迁移数据的shell脚本"
comments: true
description: "一个查询数据库迁移数据的shell脚本"
keywords: ""
---

一个我自己使用的,主要用于查询数据库迁移数据的shell脚本

```shell
#/usr/bin/bash

#author:dingxiaojiang

data="/data/data_1"
data1="/data/data_2"
log="/data/log"

#------------------ Get data ------------------
sqlcon="mysql -h <Mysql主机地址> -u root -p1234"
:>${data}

${sqlcon} -e "select memberid from db_name.table_name;" \
| awk 'BEGIN{OFS='\t'}{if(NR==1)next; print $0}' >>${data}

#echo "Get data from db_name.table_name completed."


#------------------ Handle data ------------------
sqlcon1="mysql -h <Mysql主机地址> -u root -p1234"
:>${data1}

cat ${data} | while read memberid
do
	((i=$memberid%100)) # 取余,这里是分表规则,具体需求按照自己的来
	${sqlcon1} -e "select memberid,lives from db_name.table_name_${i} where memberid=${memberid};" \
	| awk 'BEGIN{OFS='\t'}{if(NR==1)next; print $0}' >>${data1}
done

echo "Handle data completed."

#------------------ Insert data ------------------
sqlcon2="mysql -h <Mysql主机地址> -u root -p1234"
:>${log}

cat ${data1} | while read memberid lives
do
	${sqlcon2} -e "update db_name.table_name set lives=${lives} where memberid=${memberid};" \
	| awk 'BEGIN{OFS='\t'}{if(NR==1)next; print $0}' >>${log}
done


#------------------ 这是一段使用mysql load data功能的shell脚本从文件中将数据导入数据库 ------------------
#mysql -h <Mysql主机> -u root -vv -p1234 <<EOF
#use db_name;
#load data local infile '${data1}' into table table_name(memberid, avatar, mobile, type, status, videos, fans, follows, praise_videos);
#exit
#EOF

echo "Load data completed."

#------------------ Delete temp files ------------------
find /data/* -atime +5 -exec rm -f {} \;

echo "Delete temp files completed."

```



