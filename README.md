# hyperf-watch
🚀 Hyperf Watch Scripts
🚗 Make Happy to Coding
👉 快乐的热更新工具，监听文件变化自动重启Hyperf

Base on fswatch @ https://github.com/emcrisostomo/fswatch
Author: hanicc@qq.com
Version: 20190730@beta1

# 用法示例:
把watch文件放在项目根目录上
如果没有安装fswatch，先安装fswatch：
MacOS用户: brew install fswatch
Linux用户: 自行编译安装fswatch
Docker用户: 都会用Docker了，你应该知道怎么做
赋予脚本权限：
chmod +x ./watch
执行监听程序：
./watch
执行监听程序并清除监听日志:
./watch -c
退出监听程序：
Control + C
# 其它说明：
监听日志/控制台日志在./runtime/watch.log
退出监听程序会在控制台打印监听日志，方便debug
脚本默认监听整个项目文件夹，且只监听文件后缀为.php或.env
如果你希望只监听某个文件夹，请修改变量DIR
