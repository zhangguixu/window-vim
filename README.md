# 前端 window vim 折腾记

## 1. 下载gvim与基本配置

在[gvim](https://vim.sourceforge.io/download.php#pc)下载exe文件，直接在window安装即可

在windows下，vim的配置文件为_vimrc，在所安装的vim的目录下，将_vimrc打开之后，删除里面的内容，之后黏贴一下的配置，重新打开vim即可看到一个比较美观的界面了

```
set tags+=~/.vim/tags
syntax enable
syntax on
set cursorline
hi CursorLine  cterm=NONE   ctermbg=darkred ctermfg=white
hi CursorColumn cterm=NONE ctermbg=darkred ctermfg=white
filetype plugin indent on
set t_Co=256
set background=dark  "dark light "can switch it to find which is look pretty
set nocompatible                 "some plugin need it
set hlsearch                     "highlight the search
set incsearch                    "move to fit position after one char input
set nobackup                     "won't produce the backup file when save file
set nowritebackup                "won't produce the backup file when save file
set noswapfile                   "won't use swapfile
set hidden                       "can open other file when a file is not saved
set ruler                        "show ruler at the right bottom
set nowrap                       "disable auto newline
set laststatus=2                 "status bar will show anytime
set updatetime=200               "tagbar response 800ms
set showmatch matchtime=0        "show the other bracket
set wmnu wildmode=longest:full   "when in command mode can use auto complete same as bash
set expandtab tabstop=4          "expand the tab to 4 space
set si ai ci cinkeys-=0# cinoptions=g0,:0   "some indent rules
set shiftwidth=4                 "make the indent 4 length
set softtabstop=4                "backspace can del 4 space
set lcs=eol:$,tab:\|\            "display tab to green line
set backspace=indent,eol,start   "better backspace
set fileencodings=utf-8,cp936    "auto test the file is uft-8 or cp936
set fileformats=unix,dos,mac     "line feed different in different mode
set completeopt=menuone,longest
set relativenumber

set guifont=Consolas:h14 "设置字体
set clipboard=unnamed "使用windows的剪贴板

set foldmethod=syntax "用语法高亮来定义折叠
set foldlevel=100   "启动vim时不要自动折叠代码
set foldcolumn=5    "设置折叠栏的宽度
```

### 1.1 主题推荐

在此处推荐一个主题`gruvbox`，安装方法为：

1. 下载文件[gruvbox](https://github.com/morhetz/gruvbox/blob/master/colors/gruvbox.vim)，将其命名为gruvbox.vim
2. 将文件拷贝到vim安装目录下的vimfiles -> colors文件夹下
3. 在_vimrc上添加一行配置`colorscheme gruvbox`, 重启之后即可看到效果

## 2. 安装Vundle插件管理器

在windows下安装vundle比较麻烦，分为三步，vundle安装插件的原理依赖于git和curl，因此需要在windows安装这两种工具

### 2.1 安装chocolatey

[chocolatey](https://chocolatey.org/)是windows下实用的包管理器，类似于ubuntu下的`apt-get`，安装步骤如下：

在windows下打开cmd，黏贴以下命令，回车执行，即可安装chocolatey。

```
 @"%SystemRoot%\System32\WindowsPowerShell\v1.0\powershell.exe" -NoProfile -InputFormat None -ExecutionPolicy Bypass -Command "iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))" && SET "PATH=%PATH%;%ALLUSERSPROFILE%\chocolatey\bin" 
```

### 2.2 安装git和curl

如果电脑里面有了git或者curl就可以不用重复安装了，利用上一步安装的包管理工具`chocolatey`，我们只需要在cmd下执行以下命令即可完成git或者curl的安装，非常方便

```
choco install -y git
choco install -y curl
```

### 2.3 安装Vundle

完成上面的步骤之后，终于可以安装Vundle，在Vim的安装目录下，找到vimfiles，在该目录下创建bundle文件夹，进入bundler文件夹中，执行以下命令

```
git clone https://github.com/gmarik/vundle
```

clone下来的文件夹为vundle，我们将其重命名为Vundle.vim，有以下的目录结构：

Vim安装目录

    +--- vimfiles
        +--- bundle
            +--- vundle
                +--- autoload


### 2.4 配置vimrc

首先，添加一个环境变量VIM到windows下，配置

```
VIM = VIM的安装目录
```

之后，配置_vimrc，打开之后，在原有的配置基础上添加

```
"插件管理
set rtp+=$VIM/vimfiles/bundle/Vundle.vim/
call vundle#begin()

" 可以在此次安装插件
Plugin 'VundleVim/Vundle.vim'

call vundle#end()
filetype plugin indent on
```

> 配置环境变量的原因是因为通过$VIM变量可以直接找到VIM的安装根目录，注意在windows下路径之间使用/而不是\

此时重新打开vim，在normal模式下，运行命令:BundleInstall，可以看到命令成功执行，即表示成功安装vundle

### 2.5 Vundle的几点常识

Vundle安装插件通过配置文件有两种形式

1. 在`vundle#begin()`和`vundle#end()`之间，配置行`Plugin '插件名称'`
2. 直接配置一行`Bundle '插件名称'`

在normal模式下，运行

```
:PluginInstall
```

或者

```
:BundleInstall
```

都是一样的安装所有的插件

常用命令参考：

```
:BundleInstall // 安装插件
:BundleInstall! // 更新插件
:BundleClean // 卸载插件
```

## 3.1 安装常用插件

> 这一部分会不定期更新，用到什么安装什么

