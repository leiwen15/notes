# linux 常用命令
## 一、测试两台linux机器之间的网速
+ 两台机器都安装 iperf3
>+ eg. 10.28.172.27 和 10.28.172.24
>+ 安装方式：yum install -y iperf3
+ 其中一台机器启动 iperf
>+ 10.28.172.27
>+ iperf3 -s
+ 另外一台机器执行
>+ 10.28.172.24
>+ iperf3 -c 10.28.172.27 -d -t 60
## 二、linux 性能检测工具
+ linux 性能监控工具：https://blog.csdn.net/kane8202/article/details/79472811
## 三、删除创建日期大于 多少天 的数据
+ find /data/sftp/sftp/upload/mmc/ -name "mmc_2000_*.zip*" -mtime +70 -print0 |xargs -0 rm -v -f
>+ 其中， -mtime 创建时间
>+ find /data/sftp/sftp/upload/mmc/ -name "mmc_2000_*.zip*" -mtime +70 会输出多行数据
>>+ /data/sftp/sftp/upload/mmc/mmc_2000_20220316.zip
>>+ /data/sftp/sftp/upload/mmc/mmc_2000_20220317.zip
>>+ /data/sftp/sftp/upload/mmc/mmc_2000_20220318.zip
>+ find /data/sftp/sftp/upload/mmc/ -name "mmc_2000_*.zip*" -mtime +70 -print0 会将数据合并为同一行
>>+ /data/sftp/sftp/upload/mmc/mmc_2000_20220316.zip/data/sftp/sftp/upload/mmc/mmc_2000_20220317.zip/data/sftp/sftp/upload/mmc/mmc_2000_20220318.zip
>+ xargs 所擅长的正是“将标准输入作为其指定命令的参数”
>>+ 也就是将这些文件作为 rm 命令的参数
>>+ 而管道 | 只能做到 将前面的标准输入作为 后面的标准输入，无法做到命令参数
## 四、修改用户权限
+ 切换到 root 用户
+ 编辑 sudoers 文件
>+ vim /etc/sudoers
+ 添加 xxx 的权限
>+ xxx 用户执行 sudo 命令时，不需要输入密码
>>+ xxx   ALL=(ALL)    NOPASSWD: ALL
>+ xxx 用户组执行 sudo 命令时，不需要输入密码
>>+ %xxx   ALL=(ALL)    NOPASSWD: ALL
+ ps:当redhat的版本小于5.6时，需要设置用户组才可以免密码
>+ groupadd sudo
>+ usermod -G sudo xxx
## 五、在 linux 安装 conda
https://www.jianshu.com/p/914edc1de634