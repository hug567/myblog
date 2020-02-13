## 1、编译运行Linux内核

### 1.1、编译内核：

```c
sudo apt-get install gcc qemu libncurses5-dev openssl libssl-dev build-essential \
pkg-config libc6-dev bison flex libelf-dev                //安装依赖
qemu-img --version                                        //查看qemu版本

cat /proc/version                                         //查看内核版本
//下载linux-4.15
wget https://mirror.bjtu.edu.cn/kernel/linux/kernel/v4.x/linux-4.15.tar.gz
tar -xvf linux-4.15.tar.gz                                //解压linux内核
cd linux-4.15                                             //进入目录

sudo make clean; sudo make mrproper                       //清楚编译临时文件
sudo cp /boot/config-4.15.0-54-generic .config            //复制配置文件
sudo make menuconfig                                      //配置
sudo make                                                 //编译
find ./ -name "*Image*"                                   //查看Image文件
```

### 1.2、编译busybox：

```c
//下载busybox
wget https://busybox.net/downloads/busybox-1.27.2.tar.bz2
tar -xjvf busybox-1.27.2.tar.bz2  //解压busybox
cd busybox-1.27.2  //进入目录
make menuconfig  //手动配置
/* 进入第一行"Busybox Setting", 按Y选中"Build Busybox as a static binary" */
make; make install //编译
/* 所需内容在busybox-1.27.2/_install目录下 */
```

### 1.3、制作文件系统：

```c
mkdir rootfs                                              //新建文件夹
qemu-img create rootfs.img 1G                             //新建镜像文件
mkfs.ext4 rootfs.img                                      //格式化镜像文件
sudo mount -o loop rootfs.img rootfs                      //挂载镜像文件
sudo cp -r ../busybox-1.27.2/_install/* rootfs/           //复制文件
sudo vim rootfs/etc/init.d/rcS                            //新建文件并写入
#!/bin/sh
mount -t proc none /proc
mount -t sysfs none /sys
/sbin/mdev -s
sudo chmod a+x rootfs/etc/init.d/rcS                      //添加可执行权限
sudo umount rootfs                                        //卸载镜像文件
```

### 1.4、运行kernel：

```c
uname -m  //查看本机CPU架构
qemu-system-x86_64 -kernel ./linux-4.15/arch/x86_64/boot/bzImage -hda ./rootfs.img -nographic append "root=/dev/sda rootfstype=ext4 rw"
    
./qemu-4.0.1/x86_64-softmmu/qemu-system-x86_64 -kernel ./linux-4.15/arch/x86_64/boot/bzImage -hda ./rootfs.img -nographic append "root=/dev/sda rootfstype=ext4 rw"
    
qemu-system-x86_64 -M virt -cpu cortex-a15 -m 256 -kernel ./linux-4.15/arch/x86_64/boot/bzImage -nographic -append "console=ttyAMA0"
    
qemu-system-aarch64 \
    -machine virt -M virt,gic_version=3 \
    -cpu cortex-a57 \
    -machine type=virt \
    -nographic -smp 2 -m 1024 \
    -kernel ./Image \
    -hda ./rootfs.img \
    -append “console=ttyAMA0 root=/dev/vda rw crashkernel=128M nr_cpus=2”
```

### 1.5、更新至qemu 4.0：

```c
//wget https://download.qemu.org/qemu-4.0.1.tar.xz
sudo apt-get install python python3 zlib1g-dev libglib2.0-dev \
    libtool autoconf libpixman-1-dev flex bison  //安装依赖
./configure
make
sudo make install
```

### 1.7、下载arm-linux-gnueabi-gcc：

```c
wget https://armkeil.blob.core.windows.net/developer/Files/downloads/gnu-rm/9-2019q4/gcc-arm-none-eabi-9-2019-q4-major-aarch64-linux.tar.bz2










```

### 1.8、各版本gcc区别：

```c
1、arm-none-eabi-gcc：
	ARM architecture，no vendor，not target an operating system，complies with the ARM EABI，用于编译 ARM 架构的裸机系统，不适用编译 Linux 应用，不支持那些跟操作系统关系密切的函数，比如fork(2)，使用的是专用于嵌入式系统的C库newlib；

2、arm-none-linux-gnueabi-gcc：
	ARM architecture, no vendor, creates binaries that run on the Linux operating system, and uses the GNU EABI，主要用于编译ARM架构的u-boot、Linux内核、Linux应用等，实用glibc库；
















```





























