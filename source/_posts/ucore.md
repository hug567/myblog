## 1、配置环境

```c
sudo apt install qemu-utils                              //安装qemu
qemu-img --version                                       //查看qemu版本
```

## 2、编译ucore：

```C
git clone    //下载ucore
cd    //进入目录
make    //编译
make qemu    //运行
```

