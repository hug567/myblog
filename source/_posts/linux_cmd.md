### 1、基本命令

```c
```


### 2、安装卸载

```c
sudo apt install <package>                               //安装软件
dpkg -l                                                  //查看所有已安装软件
dpkg -l | grep -i <name>                                 //查看指定相关软件
sudo apt --purge remove <package>                        //删除软件及其配置文件
apt-cache search vim                                     //搜索软件
```

### 3、查找

```c
find                                                     //查找文件
    find . -name "file.c"                                //在当前目录及子目录中查找指定文件
grep
    grep -nr "string" .                                  //查找文件
```
