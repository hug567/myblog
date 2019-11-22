## 1、安装git：

```C
sudo apt install git                                     //安装git
git --version                                            //查看git版本
git config --global user.name "Huang Xing"               //设置用户名
git config --global user.email huangxing567@163.com      //设置邮箱
ssh-keygen -t rsa -C "huangxing567@163.com"              //配置SSH Key
cat ~/.ssh/id_rsa.pub                                    //查看SSH Key
```

## 2、常用操作：

### 2.1、查看状态

```C
git log                                                  //查看提交日志
git log --name-status                                    //log显示修改文件列表
git show                                                 //查看最新commit详细修改
```
