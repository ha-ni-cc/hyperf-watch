## hyperf-watch

🚀 Hyperf Watch Hot Reload Scripts

😊 Make Coding More Happy

👉 监听文件变化自动重启Hyperf

Author: hanicc@qq.com

Tips: 建议只在开发环境中使用，线上生产环境请用Docker（可以优雅热重启）。

## 使用说明:

### PHP版本（全平台通用，PHP>=7.2 && Swoole>=4.4）

基于Swoole的Process/Timer/Event实现，定时扫描文件并监听文件变动重启服务，

不依赖其它扩展，性能表现一般，全平台可用，体验较好（可在控制台直接输出运行日志）。

#### 下载watch，把文件放在项目根目录上。

#### 启动监听：

php watch

#### 启动监听并删除runtime文件夹(缓存)：

php watch -c

***

### Shell版本（不再维护，仅推荐MacOS用户使用，需要安装fswatch扩展）

基于fswatch扩展监听文件变化，性能上较好，体验一般（运行日志无法挂载在控制台上输出）。

#### 如果没有安装fswatch，需要先安装fswatch：

🍎 MacOS用户:

brew install fswatch

🤖 Linux用户: 

自行编译fswatch 👉 https://github.com/emcrisostomo/fswatch

由于能力有限，Linux基于fswatch监听有问题未完美处理，所以暂不推荐，可以使用watch.php。

#### 下载watch.sh，把文件放在项目根目录上并赋予脚本权限：

chmod +x ./watch.sh

#### 执行监听程序不清除监听日志：

./watch.sh

#### 执行监听程序并清除监听日志:

./watch.sh -c

#### 更多指令请参照帮助指南：

./watch.sh -h

***

### 退出监听：

Control + C

### 其它说明：

shell版本监听日志/控制台日志在./runtime/watch.log

shell版本退出监听程序会在控制台打印监听日志，方便debug

shell版本脚本默认监听整个项目文件夹，且只监听文件后缀为.php或.env，如需自定义监听请参照帮助指南
