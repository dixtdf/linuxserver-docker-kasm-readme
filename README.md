# linuxserver-docker-kasm-readme
这是一个关于linuxserver/docker-kasm找回登录密码的介绍
https://github.com/linuxserver/docker-kasm

# 经历
我在unraid上使用linuxserver/docker-kasm安装后没有找到密码的输出,从而诞生了这个教程,希望后来者不用费力就能找回密码

# 参考
这里使用的是官方给出的默认密码,但是官方的教程不够详尽,小白可能会踩坑
https://kasmweb.com/docs/latest/how_to/admin_account_recovery.html

# 步骤
查找我们需要修改的账户
进入到DB容器
```shell
docker exec -it kasm_db psql -U kasmapp -d kasm
```
执行sql查找我们要修改的用户
```sql
select * from users;
```
例如查找到的用户是admin那么将官方的sql的最后where部分的username改为admin即可
```sql
#官方示例
update users set pw_hash = 'fe519184b60a4ef9b93664a831502578499554338fd4500926996ca78fc7f522', salt = '83d0947a-bf55-4bec-893b-63aed487a05e', secret=NULL, set_two_factor=False, locked=False, disabled=False, failed_pw_attempts = 0 where username ='admin@kasm.local';

#修改后的
update users set pw_hash = 'fe519184b60a4ef9b93664a831502578499554338fd4500926996ca78fc7f522', salt = '83d0947a-bf55-4bec-893b-63aed487a05e', secret=NULL, set_two_factor=False, locked=False, disabled=False, failed_pw_attempts = 0 where username ='admin';
```

希望对后来者有帮助
