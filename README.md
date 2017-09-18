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

> 依此方法类推，在windows下安装主题配色都是这样的方法步骤。

## 2. 安装Vundle插件管理器

在windows下安装vundle比较麻烦，分为三步，vundle安装插件的原理依赖于git和curl，因此需要在windows安装这两种工具

### 2.1 安装chocolatey

[chocolatey](https://chocolatey.org/)是windows下实用的包管理器，类似于ubuntu下的`apt-get`，安装步骤如下：

在windows下打开cmd，黏贴以下命令，回车执行，即可安装chocolatey，这里注意要使用管理员权限。

```
 @"%SystemRoot%\System32\WindowsPowerShell\v1.0\powershell.exe" -NoProfile -InputFormat None -ExecutionPolicy Bypass -Command "iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))" && SET "PATH=%PATH%;%ALLUSERSPROFILE%\chocolatey\bin" 
```

### 2.2 安装git和curl

如果电脑里面有了git或者curl就可以不用重复安装了，利用上一步安装的包管理工具`chocolatey`，我们只需要在cmd下执行以下命令即可完成git或者curl的安装，非常方便

```
choco install -y git
choco install -y curl
```

> 这里同样需要管理员权限

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

## 3 常用插件与用法

> 这一部分会不定期更新，用到什么安装什么

在windows下安装插件大部分时候需要重新启动vim，很尴尬！

如果想多安装的插件有更多的了解可以自行搜索vim+插件名，一般在github就可以直接搜索到。

### 3.1 美观底部状态栏

安装的插件叫[vim-airline](https://github.com/vim-airline/vim-airline), 安装步骤如下：

1. 配置_vimrc, 添加以下配置，参考上面vundle安装插件的常识

    ```
    Plugin 'vim-airline/vim-airline'
    Plugin 'vim-airline/vim-airline-themes'
    ```

2. 执行:BundleInstall，安装之后重新启动即可

### 3.2 nerdTree

边栏文件管理，不用多介绍，直接在配置_vimrc，使用:BundleInstall即可

```
Bundle 'scrooloose/nerdtree'
```

配置快捷键，按F2开关边栏，浏览文件

```
" nerdTree快捷键映射
let NERDTreeWinPos='left'
let NERDTreeWinSize=30
map <F2> :NERDTreeToggle<CR>
```

### 3.3 emmet / vim-closetag

前端开发经常使用到的插件，安装还是配置_vimrc，使用:BundleInstall即可

```
Bundle 'mattn/emmet-vim'
```

配置emmet的快捷键ctrl+tab，并且使其只在特定的文件类型下才生效，单独设置tab不科学，经常使用tab进行缩进的

```
" 设置emmet快捷
let g:user_emmet_expandabbr_key = '<c-tab>'
let g:user_emmet_settings = {'indentation': '    '}
let g:user_emmet_install_global = 0
autocmd FileType html,css EmmetInstall
```

在用不到emmet的时候，可以使用`vim-closetag`进行自动关闭html、xml标签，在html文件比较大的情况下还是蛮实用的，配置如下

```
Plugin 'alvan/vim-closetag'
```

### 3.4 markdown

安装markdown插件，可以支持markdown的语法，如果需要预览则要安装额外安装其他的插件

配置_vimrc，使用:BundleInstall

```
" markdown插件
Plugin 'godlygeek/tabular'
Plugin 'plasticboy/vim-markdown'
```

### 3.5 js/css/html/json 格式化

配置_vimrc，再执行`:PluginInstall`，注意，需要有npm的支持，即在电脑上安装node环境

```
Plugin 'maksimr/vim-jsbeautify'
```

设置快捷键，配置_vimrc

```
map <c-f> :call JsBeautify()<cr>
```

即可使用ctrl+f的快捷键格式化文件

### 3.6 快速打开文件

在vim中，快速查找并打开该文件，使用ctrlp.vim，配置_vimrc，使用Vundle进行安装即可

```
Plugin 'ctrlpvim/ctrlp.vim'
```

配置快捷键，ctrl+p，打开搜索栏，可以浏览当前文件夹的文件，也可以快速打开文件

```
let g:ctrlp_map = '<c-p>'
let g:ctrlp_cmd = 'CtrlP'
```

### 3.7 多窗口

当分隔多个窗口的时候，即使用`:vsp filename`指令时，可以插件`szw/vim-maximizer`，进行窗口的最大最小化，很方便

```
Plugin 'szw/vim-maximizer'
```

配置F3为快捷键，配置如下

```
nnoremap <silent><F3> :MaximizerToggle<CR>
vnoremap <silent><F3> :MaximizerToggle<CR>gv
inoremap <silent><F3> <C-o>:MaximizerToggle<CR>
```

### 3.8 全局搜索

在windows下，全局搜索是一个很麻烦的事情，这里决定使用vim自带的`vimgrep`，但是这个命令使用起来比较麻烦，因此使用了插件`vim-easygrep`，同样使用Vundle进行安装

```
Plugin 'dkprice/vim-easygrep'
```

vim-easygrep有一些默认的快捷键，例如

```
<leader>vv 可以在当前目录下全局搜索指针选择的单词
```

例如我们要全局搜索一段字符串`str-star`，可以在可视模式下通过光标移动选择该字符串，之后按下快捷键 <leader>vv，即完成字符串的搜索，很方便

当然，我们也可以直接进行全局搜索，使用指令

```
:Grep 搜索字符串
```

全局替换也可以

```
:Replace [target] [replacement]
```

### 3.9 注释代码

实现代码的快速注释，使用的是插件`scrooloose/nerdcommenter`，配置如下

```
Plugin 'scrooloose/nerdcommenter'
```

有默认的快捷方式：

1. 注释当前行：<leader>cc
2. toggle注释：<leader>c<space>

配置了注释时空出一个字符

```
let g:NERDSpaceDelims = 1
```

### 3.10 javascript库语法高亮

安装了插件`javascript-libraries-syntax.vim`，配置如下

```
Bundle 'javascript-libraries-syntax.vim'
```

安装之后，可以设置识别的js库函数，进行语法高亮

```
let g:used_javascript_libs = 'jquery,requirejs'
```


### 3.11 光标的快速移动

快速移动光标的插件`easymotion`，安装配置如下

```
Plugin 'easymotion/vim-easymotion'
```

开启快速移动的模式 <leader><leader>w

输入高亮的字母可以调到对应的位置
