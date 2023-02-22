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
/dev/pts/X
``` 
2. redirect terminal to output
``` shell
(gdb) tty /dev/pts/Y
```

## 2 Pause mechanism
| Mechanism     | Pause                     |
| ------------- | ------------------------- |
| breakpoint    | pause execution           |
| watchpoint    | pause execution when a particular memory location changes value|
| catchpoint    | pause execution when a particular event occurs |


## 3 Command
### 3.1 Running
| Command       | Explanation               |
| ------------- | ------------------------- |
| r / run       | run program from start    |
| c / continue  | continue program from now |
| s / start     | start from main and stop  |

### 3.2 Breakpoint
| Command       | Explanation               |
| ------------- | ------------------------- |
| b / break     | set a breakpoint          |

### 3.3 Watchpoint
| Command       | Explanation               |
| ------------- | ------------------------- |
| w / watch     | set a watchpoint          |

### 3.4 Point operation
| Command              | Explanation                 |
| -------------------- | --------------------------- |
| i / info breakpoints | query information of points |
| d / delete           | delete a / all points       |
| disable              | disable points              |
| enable               | enable points               |