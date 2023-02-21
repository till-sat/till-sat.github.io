# GDB

## 0 Manual
### Started
* [软件调试的艺术](./%E8%BD%AF%E4%BB%B6%E8%B0%83%E8%AF%95%E7%9A%84%E8%89%BA%E6%9C%AF.pdf)

### Advanced
* [Debugging with GDB The GNU Source-Level Debugger](./Debugging%20with%20GDB%20The%20GNU%20Source-Level%20Debugger.pdf)

## 1 Shell
### 1.1 Debug program
``` shell
$ gdbtui xxx
```
or
``` shell
$ gdb xxx
(gdb) layout src
```

### 1.2 Terminal operation
* See [../terminal/README.md](../terminal/README.md)

### 1.3 Preventing display confusion
1. query current terminal's output
``` shell
$ tty
/dev/pts/0
``` 
2. redirect terminal to output
``` shell
(gdb) tty /dev/pts/1
```

## 2 Command
### 2.1 Running
| Command       | Explanation               |
| ------------- | ------------------------- |
| r / run       | run program from start    |
| c / continue  | continue program from now |
| s / start     | start from main and stop  |

