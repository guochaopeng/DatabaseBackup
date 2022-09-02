一: mysql的清空数据表的方式
1. truncate table_name
2. delete * from table_name;
3. drop table_name;

二：mysql定时清理表数据
从mysql5.1.6起, 增加了事件调度器(event Scheduler), 可以用作定时执行某些特定任务，
来取代原先智能由操作系统的计划任务来执行的工作
而且事件调度器可以精确到每秒钟执行一个任务.

1. 事件调度器的开关
   a, 确认是否开启  show variables like 'event_scheduler'
   b, 开启命令: set global event_scheduler = on
   
2. 创建事件<创建后默认开启>
CREATE EVENT [IF NOT EXISTS] event_name ON SCHEDULE schedule
 [ON COMPLETION [NOT] PRESERVE] [ENABLE | DISABLE] [COMMENT 'comment']

 DO sql_statement;

案例: 
1. 每分钟清空一次记录表;
   create event truncatetable2 on schedule every 60 second do truncate sortprogress;
   
2. 每天定时清空:
   create event cleartable on schedule every 1 day starts '10:40:00' do truncate table sortprogress;
