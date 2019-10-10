# hyperf-watch

🚀 Hyperf Watch Scripts

😊 Make Coding More Happy

👉 监听文件变化自动重启Hyperf

Author: hanicc@qq.com

# 使用说明:

## PHP版本，基于Swoole

### 下载watch.php，把文件放在项目根目录上

### 启动监听：

php watch.php

### 启动监听并清除代理类：

php watch.php -c


## Shell版本，基于fswatch

### 如果没有安装fswatch，需要先安装fswatch：

🍎 MacOS用户:

brew install fswatch

🤖 Linux用户: 

自行编译fswatch 👉 https://github.com/emcrisostomo/fswatch

由于能力有限，Linux基于fswatch监听有问题未完美处理，所以暂不推荐，建议使用watch.php。

### 下载watch.sh，把文件放在项目根目录上并赋予脚本权限：

chmod +x ./watch.sh

### 执行监听程序不清除监听日志：

./watch.sh

### 执行监听程序并清除监听日志:

./watch.sh -c

### 更多指令请参照帮助指南

./watch.sh -h

### 退出监听程序：

Control + C

## 其它说明：

监听日志/控制台日志在./runtime/watch.log

退出监听程序会在控制台打印监听日志，方便debug

脚本默认监听整个项目文件夹，且只监听文件后缀为.php或.env，如需自定义监听请参照帮助指南
