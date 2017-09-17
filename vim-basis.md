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

