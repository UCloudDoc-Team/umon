{{indexmenu_n>30}}

# FAQ

## 1.如何解决 监控uma内核版本过高 问题

**解决方法：**

1）修改/usr/libs/uma\_py/umacommon/umaiostat.py,在第45行增加四个ignore

``` 
43 def line_to_dict_stats(line):
44     try:
45          major, minor, Device, r_ios, r_merges, r_sec, r_ticks, w_ios, w_merges, w_sec, w_ticks, ios_pgr, tot_ticks, rq_ticks, ignore, ignore, ignore, ignore = line.split()

```

2）重启uma

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
