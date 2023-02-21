# GDB

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

