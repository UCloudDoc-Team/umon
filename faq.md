

# FAQ

## 1.Ubuntu16.0.4等系统安装uma后无法采集数据

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
