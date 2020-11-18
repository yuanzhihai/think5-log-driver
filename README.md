# think5-log-driver
think5-log-driver

## 依赖
适用于`thinkphp5.1.*`
php: >=5.6

## 安装 
1. 安装`think5-log-driver`
```sh
composer require yzh52521/think5-log-driver
```

## 使用
1. 更改配置  
在`config/log.php` 中的配置修改
```php
// 日志记录方式
// 日志通道列表

    'type'           => 'Database',
    // 大于0.05秒的sql将被记录
    'sql_time'       => 0.05,
    // 记录日志的数据库配置，即在database.php中的key
    // 如果设置该值为'default'，则使用系统数据库的实例
    'db_connect'     => '',
    // 记录慢日志查询的数据表名
    'db_table'       => 'log_sql',
    // 忽略的操作，在以下数据中的操作不会被记录
    'action_filters' => [
        // 'index/Index/list'
    ],
```

2. 创建数据库  
用于记录日志的mysql数据表,如果使用mongodb则无需创建
```sql
CREATE TABLE `th_log_sql` (
	`id` INT(10) UNSIGNED NOT NULL AUTO_INCREMENT,
	`host` CHAR(200) NOT NULL DEFAULT '',
	`uri` CHAR(200) NOT NULL DEFAULT '',
	`ip` CHAR(50) NOT NULL DEFAULT '',
	`method` CHAR(50) NOT NULL DEFAULT '',
	`module` CHAR(30) NOT NULL DEFAULT '',
	`controller` CHAR(30) NOT NULL DEFAULT '',
	`action` CHAR(50) NOT NULL DEFAULT '',
	`create_time` INT(11) NOT NULL DEFAULT '0',
	`create_date` DATETIME NULL DEFAULT NULL,
	`runtime` DECIMAL(10,3) UNSIGNED NOT NULL DEFAULT '0.000',
	`sql_list` TEXT NULL,
	`sql_source` TEXT NULL,
	PRIMARY KEY (`id`),
	INDEX `rumtime` (`runtime`)
)
COLLATE='utf8_general_ci'
ENGINE=InnoDB
AUTO_INCREMENT=1
;
```
