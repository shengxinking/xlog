#下载
https://github.com/qidasheng/xlog


#安装
./configure 
make
make install

#清理
make clean

#卸载
make uninstall


#配置编辑配置文件xlog.conf(没有默认配置，自己放哪都行，运行的时候通过-c参数指定)
[public]
#日志每行最小长度，不符合的丢弃
line_min_len = 10
#日志每行最大长度，不符合的丢弃
line_max_len = 40960
#每次发送几行日志(目前只支持一次一行，这样也能避免延迟)
line_count_per = 1
#flume sources类型为netcat对应的ip
server_addr = 10.19.1.59
#flume sources类型为netcat对应的端口
server_port = 9161
#链接flume失败重试次数
server_retry_count = 3
#链接flume失败重试时间间隔(单位为妙)
server_retry_interval = 3
#xlog日志文件路径
log_file = /var/log/xlog.log
#日志级别(暂时作用不大)
log_level = normal
#xlog监听ip(目前没用到，为以后功能预留)
listen_addr = 0.0.0.0
#xlog监听端口(目前没用到，为以后功能预留)
listen_port = 77780
#是否后台运行(yes or no)
daemonize = no

[project]
#项目名称
name = project1
#从头开始收集，还是从尾部开始收集(0结尾,1开头，未来会支持从指定行开始收集)
from_begin = 0
#项目日志文件路径
path = /data1/logs/project1_access.log
#项目类型(这个目前可以随便填，什么日志类型都支持)
type = nginx
#日志中出现如下关键就忽略掉不进行收集
ignore = 58.83.211
#已下和[public]相同配置部分如果不配置默认使用[public]部分的配置(方便所有项目都发送到一个flume收集器的情况)
line_min_len = 10
line_max_len = 40960
line_count_per = 1
server_addr = 10.19.1.59
server_port = 9163
server_retry_count = 3
server_retry_interval = 3



#支持同时收集多个项目,每个项目一个独立的进程进行，配置文件注释符号为#号
#[project]
#name = project3
#from_begin = 0
#path = /data1/logs/project3_access.log
#type = nginx
#ignore = officialssi
#server_addr = 10.19.1.59
#server_port = 9164
#server_retry_count = 3
#server_retry_interval = 3





#运行
xlog -c xlog.conf

#后台运行
配置daemonize = yes
或者
xlog -c xlog.conf -d


