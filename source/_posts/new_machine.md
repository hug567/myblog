## 1、配置源镜像：

```c
cd /etc/apt                                              //进入目录
sudo mv sources.list sources.list-ubuntu                 //备份源镜像
sudo gedit sources.list                                  //新建源镜像
deb http://mirrors.cloud.tencent.com/ubuntu/ bionic main universe restricted multiverse
deb http://mirrors.cloud.tencent.com/ubuntu/ bionic-security main universe restricted multiverse
deb http://mirrors.cloud.tencent.com/ubuntu/ bionic-updates main universe restricted multiverse
deb http://mirrors.cloud.tencent.com/ubuntu/ bionic-backports main universe restricted multiverse
deb-src http://mirrors.cloud.tencent.com/ubuntu/ bionic main universe restricted multiverse
deb-src http://mirrors.cloud.tencent.com/ubuntu/ bionic-security main universe restricted multiverse
deb-src http://mirrors.cloud.tencent.com/ubuntu/ bionic-updates main universe restricted multiverse
deb-src http://mirrors.cloud.tencent.com/ubuntu/ bionic-backports main universe restricted multiverse
sudo apt update                                          //更新源镜像
sudo apt upgrade                                         //更新软件
```
##  2、安装软件：
```C
sudo apt install vim vim-gnome git tmux zsh gcc g++ \
     make cmake python python3                           //安装软件
vim --version                                            //查看vim版本
git --version                                            //查看git版本
tmux -V                                                  //查看tmux版本
zsh --version                                            //查看zsh版本
gcc --version                                            //查看gcc版本
g++ --version                                            //查看g++版本
make --version                                           //查看make版本
cmake --version                                          //查看cmake版本
python --version                                         //查看python版本
python3 --version                                        //查看python3版本
```
## 3、配置GitHub：
```C
git config --global user.name "Huang Xing"               //设置用户名
git config --global user.email huangxing567@163.com      //设置邮箱
ssh-keygen -t rsa -C "huangxing567@163.com"              //配置SSH Key
cat ~/.ssh/id_rsa.pub                                    //查看SSH Key
```
## 4、下载配置文件：
```C
git clone git@github.com:hug567/myconfigure.git          //下载配置仓库
cp -a <...> ~                                            //复制配置文件
```

## 5、windows下Git Bash配置：

```c
//配置GitHub并下载mgconfigure仓库
将gitbash/tmux/bin下所有文件复制到.../Program Files/Git/usr/bin下
将gitbash/tmux/share下所有文件复制到.../Program Files/Git/use/share下

```

## 6、Ubuntu 18.04 install sougou：

```c

```

