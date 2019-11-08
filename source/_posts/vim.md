## 1、常用功能：

### 1）、进入编辑模式：

```c
i                                //进入编辑模式，光标不动
a                                //进入编辑模式，光标向后跳一个字符
o                                //进入编辑模式，光标下插入空行
s                                //进入编辑模式，并删除光标后一个字符
I                                //进入编辑模式，光标跳至行首
A                                //进入编辑模式，光标调至行尾
O                                //进入编辑模式，光标上插入空行
```

### 2）、常规模式文本编辑：

```c
x                                //删除光标后一个字符，同Delete
X                                //删除光标前一个字符，同Backspace
nx                               //向后删除n个字符
nX                               //向前删除n个字符
yy                               //复制光标所在行
ny                               //复制光标所在行
nyy                              //复制光标所在行向下n行
p                                //从光标下一行开始粘贴
%                                //跳转至匹配括号
dd                               //剪切光标所在行
ndd                              //剪切光标所在行向下n行
u                                //撤销
.                                //重复
v                                //进入VISUAL模式
hjkl                             //左下上右选中文本，同方向键
^ / HOME                         //选中光标至行首
$ / END                          //选中光标至行尾
d                                //剪切
y                                //复制
p                                //粘贴
^ / HOME                         //选中光标至行首
$ / END                          //选中光标至行尾
ggyG                             //全部复制进默认寄存器
:n1,n2d                          //删除n1-n2行内容
```

### 3）、跳转翻页：

```c
gg                               //光标移到至第一行
G                                //光标移动至最后一行
nG                               //光标移动至第n行
nEnter                           //光标向下移动n行
Ctrl + e                         //屏幕向上翻页一行
Ctrl + y                         //屏幕向下翻页一行
```

### 4）、显示分屏：

```c
:sp                              //横向分屏
:vs                              //竖向分屏
ctrl + w   w                     //各窗口循环跳转
ctrl + w   h                     //跳转至左侧窗口
ctrl + w   j                     //跳转至下方窗口
ctrl + w   k                     //跳转至上方窗口
ctrl + w   l                     //跳转至右侧窗口
ctrl + w   <                     //窗口向左缩放
ctrl + w   >                     //窗口向右缩放
ctrl + w   +                     //窗口向上缩缩
ctrl + w   -                     //窗口向下缩放
10, ctrl + w   <                 //窗口向左缩放10列
10, ctrl + w   >                 //窗口向右缩放10列
10, ctrl + w   +                 //窗口向上缩缩10行
10, ctrl + w   -                 //窗口向下缩放10行
ctrl + w   =                     //窗口尺寸恢复均等
```

### 5）、跨进程复制：

```c
vim --version | grep "clipboard"     //查看是否支持系统剪切板
sudo apt-get install vim-gnome       //安装图像化vim
v                                    //进入VISUAL模式，方向键选中
"+y                                  //复制进“+”寄存器
"+yG                                 //全文复制进“+”寄存器
"+p                                  //从“+”寄存器粘贴
:reg                                 //查看寄存器内容
```

### 6）、搜索替换：

```C
/word                            //向光标之下搜索
?word                            //向光标之上搜索
/word\c                          //大小写不敏感
n/N                              //向下/上查找匹配
:n1,n2s/word1/word2/g            //在n1至n2行间将word1替换为word2
:n1,n2s/word1/word2/gc           //替换前需确认
:%s/word1/word2/gc               //全局搜索替换
shift + *                        //搜索单词
.*\[]^$                          //需转移字符
```

### 7）、显示比较：

```C
:set nu                          //显示行号
:set nonu                        //隐藏行号
:set list                        //显示tab
:set nolist                      //隐藏tab
:noh                             //退出搜索高亮
:source ~/.vimrc                 //更新配置文件
:hi / :highlight                 //查看当前颜色配置
:f / Ctrl + G                    //查看文件名
:pwd                             //查看父目录
:diffthis                        //比较文件，在打开的两个文件中分别执行
```

### 8）、多行注释：
```C
//-----多行注释---------//
ESC                              //退出至常规模式，光标放在行首
Ctrl + V                         //进入VISUAL BLOCK模式
nj                               //选中光标往下n行
Shift + I                        //进入插入模式
//、#                            //输入注释符
ESC                              //退出(等一会)
//-----取消多行注释-----//
ESC                              //退出至常规模式，光标放在行首
Ctrl + V                         //进入VISUAL BLOCK模式
nj                               //选中光标往下n行
x或d                             //按块删除
ESC                              //退出
```

## 2、vim中使用正则表达式：

```C
\n                               //换行
\t                               //tab
\*                               //重复0次或多次
\+                               //重复1次或多次
\?                               //匹配0次或1次
\(、\)                           //小括号转义
\s                               //空白符
^                                //匹配行首
$                                //匹配行尾
:%s/\s\+$//gc                    //删除行尾空白符
:10,41s/^\(\t*\)    /\1\t/gc     //行首每4个空格替换成tab
```

## 3、vim脚本：

```c
g: varname                       //变量为全局变量
s: varname                       //变量的范围为当前的脚本文件
w: varname                       //变量的范围为当前的编辑器窗口
t: varname                       //变量的范围为当前的编辑器选项卡
b: varname                       //变量的范围为当前的编辑器缓冲区
l: varname                       //变量的范围为当前的函数
a: varname                       //变量是当前函数的一个参数
v: varname                       //变量是 Vim 的预定义变量
```

## 4、vim插件：

### 1）、Pathgyen：离线插件管理器

```c
//下载地址：https://github.com/tpope/vim-pathogen/
//下载到目录：~/.vim/autoload/.vim
//在~/.vimrc中加入：
execute pathogen#infect()
syntax on
filetype plugin indent on
```

### 2）、NERDTree：显示目录树

```C
//地址：https://github.com/scrooloose/nerdtree
cd ~/.vim/bundle                                    //进入vim插件目录
git clone git@github.com:scrooloose/nerdtree.git    //下载NERDTree
//使用：在目录树中操作节点
ctrl + w   =                     //窗口尺寸恢复均等
:NERDTreeToggle                  //切换开、关目录树
m                                //进入NERDTree Menu
    a                               //新建节点
    d                               //删除节点
    m                               //重命名节点
R                                //刷新目录树
I                                //切换显示隐藏节点
U                                //将根节点设为上级目录
C                                //将根节点设为当前节点
```

### 3）、Taglist：显示函数列表（需ctags支持）

```C
sudo apt install ctags                                  //安装ctags
git clone git@github.com:vim-scripts/taglist.vim.git    //下载taglist
cp taglist.txt ~/.vim/doc                               //复制taglist.txt
cp taglist.vim ~/.vim/pugin                             //复制taglist.vim
```

### 4）supertab：自动补全

```C
//下载：https://github.com/ervandew/supertab
cd ~/.vim/bundle	                                //进入目录
git clone git@github.com:ervandew/supertab.git          //下载supertab
```

### 5）astyle：格式化代码

```C
sudo apt install astyle          //安装astyle
astyle --version                 //查看astyle版本
:%!astyle --style=kr             //格式化当前文件
:1,40!astyle --style=kr          //格式化指定区域
```

### 6）ctags：函数跳转

```C
sudo apt install ctags           //安装ctags
ctags --version                  //查看ctags版本
ctags -R *                       //递归生产tags文件
Ctrl + ]                         //(vim中)跳转至定义
Ctrl + T                         //(vim中)返回
```

## 5、下载配色主题：

```C
//下载：[http://www.easycolor.cc/](http://www.easycolor.cc/)
cd ~/.vim/colors                 //放入指定目录(molokai.vim)
colorscheme molokai              //在~/.vimrc中设置
```