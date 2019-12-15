##  1、安装git：

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
git show <commitID>                                      //查看指定commit详细修改
git show <commitID> <filename>                           //查看指定commit中某个文件详细修改
//统计提交代码
git log --author="Huang Xing" --pretty=tformat: --numstat | gawk \
'{ add += $1: subs += $2: loc += $1 - $2} END \
{printf "added lines: %s removed lines: %s total lines: %s\n", add, subs, loc }' -
//查看详细commit信息
git log --oneline --graph --pretty=format:'%C(yellow)%h %Cred[%an]%Creset %Cblue[%ad]%Creset %s %Cgreen(%cr)%Cred%d' --date=format:'%Y-%m-%d %H:%M:%S' -n 100
```

### 2.2、本地分支管理

```C
git branch                                               //查看本地所有分支
git branch -vv                                           //查看本地分支关联的远端分支
git branch dev --set-upstream-to=origin/dev              //设置本地分支关联远端分支
git branch -a                                            //查看本地和远端所有分支
git checkout -b dev                                      //新建并切换分支
git checkout dev                                         //新建本地分支
git branch dev                                           //切换本地分支
git checkout -b dev origin/dev                           //新建本地分支并追踪远端
git merge dev                                            //合并本地分支dev至当前分支
git branch -d dev                                        //删除本地分支
git branch -D dev                                        //强制删除本地分支
git branch -m <newname>                                  //重命名当前分支
//----------取回远端分支-----------------------------------------------------//
git fetch origin master                                  //取回远端master分支至本地
git log -p FETCH_HEAD                                    //查看取回的更新信息
git diff master origin/master                            //比较本地分支与远端分支
git rebase master                                        //线性合并取回的远端分支至当前分支
//----------不commit切换分支-------------------------------------------------//
git stash                                                //暂存未add更改
git stash list                                           //查看暂存列表
git chechout <branch2>                                   //切换分支
git stash pop                                            //取出暂存
git stash drop stash@{0}                                 //删除stash第一个队列
git stash clear                                          //清空stash所有内容
```

### 2.3、远端分支管理

```C
git push origin HEAD:master                              //推送本地分支至远端
git push origin HEAD:master -f                           //强制推送本地分支至远端
git branch -r                                            //查看所有远端分支
git push --delete origin <branch>                        //删除远端分支
//----------重命名远端分支-------------------------------------------------//
git push --delete origin <branch>                        //删除远端分支
git branch -m <newname>                                  //重命名本地分支
git push origin HEAD:<newname>                           //提送至远端分支
```

### 2.4、commit操作

```C
//----------合并至最近一次commit-------------------------------------------//
git add <file>                                           //添加文件
git commit -s --amend                                    //追加至最新commit
//----------合并至指定commit----------------------------------------------//
git add <file>                                           //添加文件
git stash                                                //暂存
git log --oneline                                        //查看指定commit的ID
git rebase <ID>^ --interactive                           //移动HEAD至指定ccommit
[Operate]: first 'pick' -> 'edit', Esc, :wq              //首行'pick'改为'edit'，保存并退出
git stash pop                                            //取出暂存
git add <file>                                           //添加文件
git commit --amend                                       //追加至指定commit
git rebase --continue                                    //移动HEAD至最新commit
[Condition]: if there is conflict                        //如果有冲突
    []: edit conflit file                                //解决冲突
    git add <file>                                       //添加文件
    git commit --amend                                   //追加至指定commit
    git rebase --continue                                //移动HEAD至最新commit
//----------回退至指定commit----------------------------------------------//





```
