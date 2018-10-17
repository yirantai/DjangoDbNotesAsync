# DjangoDbNotesAsync
背景：最近接手了一个项目，但mysql中所有表，字段都没有备注，查询了Django框架好像不带这个功能，遂决定自己实现一个。
1.这是一个基于Django框架的安装包，使用前请确保已经正确安装了Django框架。
2.此包用于将Django项目中的Model表的注释，字段的注释(help_text)同步到数据库(此案例使用的是mysql5.7，sqlite，postgres并未经过测试)。
3.为求数据库中表和字段的注释简洁，此安装包中仅同步必要的字段，对于主键，外键，默认不添加备注。
4.仅会同步已经添加到INSTALLED_APPS中的APP model的备注到数据库。

### 使用方法:
1. 将DjangoDbNotesAsync添加到django项目中的INSTALLED_APPS
2. 在django项目目录，执行python manage.py db_notes_async

### 执行输出：
1.正常输出：
  ```
  正在修改表user
  正在修改表account
  正在修改表account_type
  正在修改表group
  正在修改表profile
  ...
  ```
2.异常输出：
  ```
  alter table error: alter table user comment "用户表" 
  ```
  ```
  altert table column error: alter table `procurement_statistic` modify column `unit_price_differ` decimal(11, 2) COMMENT "调整后采购单价差值"
  ```
  如遇异常输出，请检查model中字段设置，修改后手动执行。
  
### 联系作者：
  email: 896275756@qq.com
  如您有好的意见或建议，请发邮件给我，您的意见或建议将会体现在下一次的版本更新里。
