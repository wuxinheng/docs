命令

| APPEND  | 如果 key 已经存在，并且值为字符串，那么这个命令会把 value 追加到原来值（value）的结尾。 如果 key 不存在，那么它将首先创建一个空字符串的key，再执行追加操作，这种情况 APPEND将类似于SET 操作。执行之后会返回字符串长度。 |      |
| ------- | ------------------------------------------------------------ | ---- |
| DBSEIZE | 返回数据库键数                                               |      |
| FLUSHDB | 删除数据库所有键                                             |      |
| EXISTS  | 返回key是否存在。1:存在；0:不存在                            |      |

C#操作Redis提示没有权限解决办法

需要更改配置文件，使用命令行

cmd  cd  Redis安装目录 运行 redis-cli.exe

输入config set stop-writes-on-bgsave-error no

127.0.0.1:6379> config set stop-writes-on-bgsave-error no

redis设置密码

​                127.0.0.1:6379> config get requirepass  #查询账号密码 "requirepass"    #账号 ""		      #密码              

​                config set requirepass kwz  #ok后执行下一步 auth kwz                    #ok后重启服务              

将redis设置windows服务：

redis目录下执行Cmd命令

redis-server.exe --service-install redis.windows.conf --loglevel verbose

设置完成后将现有进程中的先关闭，再执行命令，不然会冲突

将端口开放更改配置文件：6379，云服务器不要忘记安全组

redis.windows.conf

修改：将   #bind 127.0.0.1  改为 0.0.0.0

protected-mode no