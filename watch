#!/usr/bin/env php
<?php
/**
 * Hyperf Watch Hot Reload Scripts
 * User: hanicc@qq.com
 * Date: 2019/11/12
 * Time: 下午16:00
 * Modify From https://github.com/leocavalcante/dwoole/blob/master/dev/watch.php
 */

# PHP Bin File PHP程序所在路径（默认自动获取）
const PHP_BIN_FILE = 'which php';
# Watch Dir 监听目录（默认监听脚本所在的根目录）
const WATCH_DIR = __DIR__ . '/';
# Watch Ext 监听扩展名（多个可用英文逗号隔开）
const WATCH_EXT = 'php,env';
# Exclude Dir 排除目录（不监听的目录，数组形式)
const EXCLUDE_DIR = ['vendor'];
# Entry Point File 入口文件
const ENTRY_POINT_FILE = './bin/hyperf.php';
# PID File Path PID文件路径
const PID_FILE_PATH = './runtime/hyperf.pid';
# Scan Interval 扫描间隔（毫秒，默认2000）
const SCAN_INTERVAL = 2000;

if (!function_exists('exec')) {
    echo "[x] 请取消禁用exec函数" . PHP_EOL;
    exit(1);
}

define('PHP', PHP_BIN_FILE == 'which php' ? exec('which php') : PHP_BIN_FILE);

if (!file_exists(PHP)) {
    echo "[x] PHP bin (" . PHP . ") 没有找到，请确认路径正确?" . PHP_EOL;
    exit(1);
}

if (!file_exists(ENTRY_POINT_FILE)) {
    echo "[x] 入口文件 (" . ENTRY_POINT_FILE . ") 没有找到，请确认文件存在?" . PHP_EOL;
    exit(1);
}

use Swoole\Process;
use Swoole\Timer;
use Swoole\Event;

swoole_async_set(['enable_coroutine' => false]);
$hashes = [];
$serve = null;
echo "🚀 Start @ " . date('Y-m-d H:i:s') . PHP_EOL;
start();
state();
Timer::tick(SCAN_INTERVAL, 'watch');

function start()
{
    // 关闭监听进程后，重新打开进程
    if (file_exists(PID_FILE_PATH) &&  $pid = @file_get_contents(PID_FILE_PATH)) {
        @posix_kill($pid);
    }

    global $serve;
    $serve = new Process('serve', true);
    $serve->start();
    if (false === $serve->pid) {
        echo swoole_strerror(swoole_errno()) . PHP_EOL;
        exit(1);
    }
    Event::add($serve->pipe, function ($pipe) use (&$serve) {
        $message = @$serve->read();
        if (!empty($message)) {
            echo $message;
        }
    });
}

function watch()
{
    global $hashes;
    foreach ($hashes as $pathname => $current_hash) {
        if (!file_exists($pathname)) {
            unset($hashes[$pathname]);
            continue;
        }
        $new_hash = file_hash($pathname);
        if ($new_hash != $current_hash) {
            change();
            state();
            break;
        }
    }
}

function state()
{
    global $hashes;
    $files = php_files(WATCH_DIR);
    $hashes = array_combine($files, array_map('file_hash', $files));
    $count = count($hashes);
    echo "📡 Watching $count files..." . PHP_EOL;
}

function change()
{
    global $serve;
    echo "🔄 Restart @ " . date('Y-m-d H:i:s') . PHP_EOL;
    Process::kill($serve->pid);
    start();
}

function serve(Process $serve)
{
    $opt = getopt('c');
    # if (isset($opt['c'])) echo exec(PHP . ' ' . ENTRY_POINT_FILE . ' di:init-proxy') . '..' . PHP_EOL;
    if (isset($opt['c'])) del_dir('./runtime/container');
    $serve->exec(PHP, [ENTRY_POINT_FILE, 'start']);
}

function file_hash(string $pathname): string
{
    $contents = file_get_contents($pathname);
    if (false === $contents) {
        return 'deleted';
    }
    return md5($contents);
}

function php_files(string $dirname): array
{
    $directory = new RecursiveDirectoryIterator($dirname);
    $filter = new Filter($directory);
    $iterator = new RecursiveIteratorIterator($filter);
    return array_map(function ($fileInfo) {
        return $fileInfo->getPathname();
    }, iterator_to_array($iterator));
}

function del_dir($path)
{
    if (is_dir($path)) {
        //扫描一个目录内的所有目录和文件并返回数组
        $dirs = scandir($path);
        foreach ($dirs as $dir) {
            //排除目录中的当前目录(.)和上一级目录(..)
            if ($dir != '.' && $dir != '..') {
                //如果是目录则递归子目录，继续操作
                $sonDir = $path . '/' . $dir;
                if (is_dir($sonDir)) {
                    //递归删除
                    del_dir($sonDir);
                    //目录内的子目录和文件删除后删除空目录
                    @rmdir($sonDir);
                } else {
                    //如果是文件直接删除
                    @unlink($sonDir);
                }
            }
        }
        @rmdir($path);
    }
}

class Filter extends RecursiveFilterIterator
{
    public function accept()
    {
        if ($this->current()->isDir()) {
            if (preg_match('/^\./', $this->current()->getFilename())) {
                return false;
            }
            return !in_array($this->current()->getFilename(), EXCLUDE_DIR);
        }
        $list = array_map(function (string $item): string {
            return "\.$item";
        }, explode(',', WATCH_EXT));
        $list = implode('|', $list);
        return preg_match("/($list)$/", $this->current()->getFilename());
    }
}
