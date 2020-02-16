## 1、编译运行Linux内核

### 1.1、下载arm-none-linux-gnueabi-gcc：

```c
wget https://armkeil.blob.core.windows.net/developer/Files/downloads/gnu-rm/9-2019q4/gcc-arm-none-eabi-9-2019-q4-major-aarch64-linux.tar.bz2
/* 在~/.bashr和~/.zshrc中添加： */
export PATH="$HOME/tools/arm-2014.05/bin:$PATH"
source ~/.bashrc                                          //更新bash配置
source ~/.zshrc                                           //更新zsh配置
arm-none-linux-gnueabi-gcc --version                      //查看版本，验证路径设置正确
```

### 1.2、编译内核：

```c
sudo apt-get install gcc qemu libncurses5-dev openssl libssl-dev build-essential \
pkg-config libc6-dev bison flex libelf-dev                //安装依赖
qemu-img --version                                        //查看qemu版本

cat /proc/version                                         //查看内核版本
//下载linux-4.15
wget https://mirror.bjtu.edu.cn/kernel/linux/kernel/v4.x/linux-4.15.tar.gz
tar -xvf linux-4.15.tar.gz                                //解压linux内核
cd linux-4.15                                             //进入目录
make clean; make mrproper

//sudo make clean; sudo make mrproper                       //清楚编译临时文件
//sudo cp /boot/config-4.15.0-54-generic .config            //复制配置文件
//sudo make menuconfig                                      //配置
//sudo make                                                 //编译

/* 配置及编译： */
make ARCH=arm CROSS_COMPILE=arm-none-linux-gnueabi- vexpress_defconfig
make ARCH=arm CROSS_COMPILE=arm-none-linux-gnueabi-
find ./ -name "*Image*"                                     //查看Image文件
/* 无文件系统启动验证： */
qemu-system-arm -M virt -cpu cortex-a15 -m 256 -kernel arch/arm/boot/zImage -nographic -append "console=ttyAMA0"
```

### 1.3、编译busybox：

```c
//下载busybox
wget https://busybox.net/downloads/busybox-1.27.2.tar.bz2
tar -xjvf busybox-1.27.2.tar.bz2  //解压busybox
cd busybox-1.27.2  //进入目录
make ARCH=arm CROSS_COMPILE=arm-none-linux-gnueabi- menuconfig  //手动配置
/* 进入第一行"Busybox Setting", 按Y选中"Build Busybox as a static binary" */
make ARCH=arm CROSS_COMPILE=arm-none-linux-gnueabi- //编译
make ARCH=arm CROSS_COMPILE=arm-none-linux-gnueabi- install //安装
/* 所需内容在busybox-1.27.2/_install目录下 */
```

### 1.4、制作文件系统：

```c
mkdir rootfs                                              //新建文件夹
cd rootfs                                                 //
sudo cp -rf ../busybox-1.27.2/_install/* ./               //复制文件
sudo mkdir proc sys dev etc etc/init.d                    //
sudo vim ./etc/init.d/rcS                                 //新建文件并写入
/*-------------------------------------------------------*/
#!/bin/sh
mount -t proc none /proc
mount -t sysfs none /sys
/sbin/mdev -s
/*-------------------------------------------------------*/
sudo chmod a+x ./etc/init.d/rcS                           //添加可执行权限
find . | cpio -o --format=newc > ../qemu_rootfs.img       //制作文件系统
cd ..                                                     //返回上层目录
gzip -c rootfs.img > rootfs.img.gz                        //压缩文件系统
```

### 1.5、运行kernel：

```c
qemu-system-arm \
    -M virt  \
    -smp 1 \
    -m 256 \
    -kernel ./arch/arm/boot/zImage \
    -initrd ../rootfs.img.gz \
    -nographic \
    -append "root=/dev/mtdblock0 rdinit=sbin/init console=ttyAMA0 noapic"

qemu命令：
-M <machine> : 机器型号
-cpu <model> : cpu模式
-smp n : cpu个数
-m 256 : 内存大小(MB)
-kernel <Image> : 内核镜像
-hda/-hdb/-hdd/-hdc <rootfs> : 虚拟机系统安装文件
-nographic : 不使用图形界面
-append : 内核命令行
	init : 文件系统启动后执行的linux的第一个进程
	root : 指定根文件系统设备
	console : 指定终端
```

### 1.6、更新至qemu 4.0：

```c
wget https://download.qemu.org/qemu-4.0.1.tar.xz          //下载qemu 4.0
sudo apt-get install python python3 zlib1g-dev libglib2.0-dev \
    libtool autoconf libpixman-1-dev flex bison           //安装依赖
./configure                                               //配置
make                                                      //编译
sudo make install                                         //安装
```

## 2、各版本gcc区别：

```c
1、arm-none-eabi-gcc：
	ARM architecture，no vendor，not target an operating system，complies with the ARM EABI，用于编译 ARM 架构的裸机系统，不适用编译 Linux 应用，不支持那些跟操作系统关系密切的函数，比如fork(2)，使用的是专用于嵌入式系统的C库newlib；

2、arm-none-linux-gnueabi-gcc：
	ARM architecture, no vendor, creates binaries that run on the Linux operating system, and uses the GNU EABI，主要用于编译ARM架构的u-boot、Linux内核、Linux应用等，实用glibc库；
```





























