# dble-DDL

## Setting

当表在做DDL的时候，不允许对该表做其他操作
> mysql> select * from account limit 10;
ERROR 4006 (HY000):SCHEMA[surl],TABLE[account]is doing DDL.

## Root Cause

对于在dble端操作时，当表在做DDL的时候，dble中只要有DDL线程获取到DDL锁，在正式开始执行之后，所有对于该表的查询都无法进行；但是在单机mysql上是被允许的。  
dble之所以这样的操作未被允许，主要是涉及到并发和顺序的问题，因为后端节点有多个，所以时序问题比较困扰。
