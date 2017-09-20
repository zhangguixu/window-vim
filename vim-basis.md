# 常用的VIM操作

## 分屏

```
:sp filename " 上下分屏
:vsp filename " 左右分屏
```

关闭当前窗口（按键序列）

```
ctrl+w c
```

移动分屏

```
ctrl+w h/j/k/l
```

## 执行外部命令

在vim中，可以执行git、npm命令，在命令行模式下，加上`!`即可，如

```
!npm run develop
!git add .
```

## 多标签页面

```
:tabe / :tabnew 新建一个标签页
:tabo / :tabonly :tabe / :tabnew 新建一个标签页
:tabc / :tabclose 关闭当前标签页
:tabn / :tabl / :tabfir / :tabN 标签页切换
```

## 设置自己常用的快捷键

### f5

一键运行`npm run develop`，并且在vim中打开一个缓冲区，记录运行的结果。

原理：利用exe在vim中执行命令，并且利用管道来获取外部命令运行的结果，使用new开启一个缓冲区，最后通过将缓冲区设置

```
" 执行npm run develop，效果是执行之后，将log打到vim的缓存区
function BuildProject ()
    " 先保存全部，再执行构建命令
    exe 'wa'
    exe 'new | setlocal buftype=nofile bufhidden=hide | read !npm run develop '
endfunction
nmap <silent><F5> :call BuildProject()<CR>
```

### space + w

normal模式下，保存全部，配置如下，此外，此配置还更改了<leader>的映射，使其更加的顺手

``` 
" 将 <leader> 映射到<space>
let mapleader = "\<space>"
let g:mapleader = "\<space>"

" 保存全部，不然打开的项目文件一多有时间就忘记保存了
nnoremap <leader>w :wa <CR>
```
