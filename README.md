## hyperf-watch

🚀 Hyperf Watch Hot Reload Scripts

😊 Make Coding More Happy

👉 监听文件变化自动重启Hyperf

Author: hanicc@qq.com

Tips: 只建议在开发环境中使用，如果对您有帮助，请给项目一个Star，谢谢！

## 使用说明:

PHP>=7.2 && Swoole>=4.4（如果你是Windows系统并使用了WSL，建议PHP开启pcntl扩展）

基于Swoole的Process/Timer/Event实现，定时扫描文件并监听文件变动重启服务

#### 下载watch文件（为了使用方便，保存文件时建议不要保留扩展名）：

[下载地址->请右键另存为，并去掉扩展名.txt](https://raw.githubusercontent.com/ha-ni-cc/hyperf-watch/master/watch)

#### 启动监听：

请把文件watch放在项目根目录上，并在项目根目录下启动命令行终端
 ```
php watch
```
#### 启动监听并删除代理类缓存(./runtime/container)：
```
php watch -c
```
#### 退出监听：
```
Control + C
```

***

## 捐赠：

如果您喜欢这个脚本，要不给我来杯枸杞茶吧！请在打赏时备注您的称呼，方便致谢！

![lELWmd.jpg](https://s2.ax1x.com/2019/12/27/lELWmd.jpg)
