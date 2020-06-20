## hyperf-watch

🚀 Hyperf Watch Hot Reload Scripts

😊 Make Coding More Happy

👉 监听文件变化自动重启Hyperf

Author: hanicc@qq.com

Tips: 只建议在开发环境中使用，如果对您有帮助，请给项目一个Star，谢谢！

Gitee仓库: https://gitee.com/hanicc/hyperf-watch

## 使用说明:

建议PHP>=7.2 && Swoole>=4.4，php.ini需要开启exec方法

基于Swoole的Process/Timer/Event实现，定时扫描文件并监听文件变动重启服务

#### 下载文件：

【Windows】

下载完成后请拷贝到项目根目录上：

[下载地址->请右键另存为，并删去扩展名.txt](https://gitee.com/hanicc/hyperf-watch/raw/master/watch)

【MacOS or Linux】

在项目根目录下启动终端控制台：
```sh
wget -O watch https://gitee.com/hanicc/hyperf-watch/raw/master/watch
```

#### 启动监听：
 ```sh
php watch
```

#### 启动监听并删除代理类缓存(./runtime/container)：
```sh
php watch -c
```

#### 退出监听：
```sh
Control + C
```
#### 默认配置（打开watch文件，可自行修改）:
```php
# PHP Bin File PHP程序所在路径（默认自动获取）
const PHP_BIN_FILE = 'which php';
# Watch Dir 监听目录（默认监听脚本所在的根目录）
const WATCH_DIR = __DIR__ . '/';
# Watch Ext 监听扩展名（多个可用英文逗号隔开）
const WATCH_EXT = 'php,env';
# Exclude Dir 排除目录（不监听的目录，数组形式)
const EXCLUDE_DIR = ['vendor', 'runtime', 'public'];
# Entry Point File 入口文件
const ENTRY_POINT_FILE = __DIR__ . '/bin/hyperf.php';
# Start Command 启动命令
const START_COMMAND = [ENTRY_POINT_FILE, 'start'];
# PID File Path PID文件路径
const PID_FILE_PATH = __DIR__ . '/runtime/hyperf.pid';
# Scan Interval 扫描间隔（毫秒，默认2000）
const SCAN_INTERVAL = 2000;
# Console Color 控制台颜色
const CONSOLE_COLOR_DEFAULT = "\033[0m";
const CONSOLE_COLOR_RED = "\033[0;31m";
const CONSOLE_COLOR_GREEN = "\033[0;32m";
const CONSOLE_COLOR_YELLOW = "\033[0;33m";
const CONSOLE_COLOR_BLUE = "\033[0;34m";
```
