## DjangoDbNotesAsync
```
背景：最近接手了一个项目，但mysql中所有表，字段都没有备注阅读有诸多不便，查询了Django框架好像不带这个功能，遂决定自己实现一个。
1.此安装包基于Django框架，并使用django.core.management.base中的BaseCommand类，使用前请确保已经正确安装了Django框架。
2.此包用于将Django项目中的Model表的注释，字段的注释(help_text)同步到数据库(此案例使用的是mysql5.7；sqlite，postgres等并未经过测试)。
3.为求数据库中表和字段的注释简洁，此安装包中仅同步必要的字段，对于主键，外键等非必要字段默认不添加备注(如有需求后期版本会添加。)。
4.仅会同步已经添加到INSTALLED_APPS中的APP model的备注到数据库。
```

版本说明：
v1.0.2: 优化表，字段备注写入方式；优化控制台输出信息。
v1.0.1: 优化写入方式。
v1.0.0: 初始版本发布。

### 安装：
  pip install DjangoDbNotesAsync

### 使用方法:
```
1. 将DjangoDbNotesAsync添加到django项目中的INSTALLED_APPS
2. 将要同步的app添加到INSTALLED_APPS中
3. 在django项目目录，执行python manage.py db_notes_async
```
### 使用备注：
```
1.同步表名称时，优先取表模型的Meta属性中verbose_name中字段。如果没取到会取表.__doc__属性。
2.仅同步字段中help_text不为空属性的字段。
```

### 执行输出：
1.正常输出：
  ```
表:【user】, 注释信息: 【用户表】, 添加成功......
表:【user】, 字段: 【created_at】, 注释信息: 【创建时间】, 添加成功......
表:【user】, 字段: 【updated_at】, 注释信息: 【更新时间】, 添加成功......
表:【user】, 字段: 【created_timestamp】, 注释信息: 【创建时间戳】, 添加成功......
表:【user】, 字段: 【is_deleted】, 注释信息: 【是否删除】, 添加成功......
表:【user】, 字段: 【username】, 注释信息: 【用户名】, 添加成功......
表:【user】, 字段: 【phone】, 注释信息: 【手机号码】, 添加成功......
  ...
  ```
2.异常输出：
  ```
  错误信息:  表: user, 字段: created_timestamp, 注释信息: 创建时间戳, sql: alter table `carrier_leaderrole` modify column `created_timestamp` float(None) COMMENT "创建时间戳" ，原因rror in your SQL syntax; check the manual that corresponds to your MySQL server version for the right syntax to use near \'None) COMMENT "创建时间戳"\' at line 1')
  ```
  如遇异常输出，请检查model中字段设置，修改后手动执行。
  
#### 联系作者：
  email: 896275756@qq.com
  如您有好的意见或建议，请发邮件给我，您的意见或建议将会体现在下一次的版本更新里。
