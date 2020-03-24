

# FAQ

## 1.如何解决 监控uma因内核版本过高 报错问题

**问题现象**：内核版本大于4.18时，报错too many values to unpack 

**问题原因**：由于4.18+内核在/proc/diskstats文件上有变动，由原来的14行变为18行，导致在解析时不兼容（uma1.1.4及以下版本会存在此类问题） 

**解决方法：**

- **处理方案1**：建议您升级到uma1.1.5及以上版本（详见：[新版监控代理安装](https://docs.ucloud.cn/umon/agent )），已修复此类问题；
- **处理方案2**：在uma版本不升级的情况下，可以通过修改/usr/libs/uma\_py/umacommon/umaiostat.py,在第45行增加四个ignore（见下述），修改后重启uma，也可解决。

``` 
43 def line_to_dict_stats(line):
44     try:
45          major, minor, Device, r_ios, r_merges, r_sec, r_ticks, w_ios, w_merges, w_sec, w_ticks, ios_pgr, tot_ticks, rq_ticks, ignore, ignore, ignore, ignore = line.split()

```



## 2.Ubuntu16.0.4等系统安装uma后无法采集数据

> Ubuntu16.0.4等系统默认未支持Python2.x相关版本

**解决方法：**

1）卸载uma

    dpkg -P uma

2）安装Python2.x相关版本

``` 
sudo apt-get install python2.7
sudo apt-get install python-pip

```

3）重新安装uma
