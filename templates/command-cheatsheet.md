# ⌨️ 命令行速查表（定制版 · 10个命令）

> **记住一个类比**：命令行 = 直接给电脑打字下指令，比鼠标点点点更精确。

---

## 核心10命令

| # | 命令 | 作用（一句话） | 类比 | 示例 |
|:---|:---|:---|:---|:---|
| 1 | `pwd` | 看看自己在哪个文件夹 | 📍 GPS定位 | `pwd` |
| 2 | `ls` / `dir` | 看看当前文件夹里有什么 | 👀 环顾四周 | `ls` |
| 3 | `cd 文件夹名` | 进入一个文件夹 | 🚶 进房间 | `cd Desktop` |
| 4 | `cd ..` | 回到上一级文件夹 | 🚶 出房间 | `cd ..` |
| 5 | `mkdir 名字` | 新建一个文件夹 | 🏗️ 建新房间 | `mkdir test` |
| 6 | `echo "文字"` | 输出一行字 | 📢 喊一嗓子 | `echo "hello"` |
| 7 | `cat 文件名` | 查看文件内容 | 📖 读便条 | `cat note.txt` |
| 8 | `rm 文件名` | 删除文件 ⚠️ | 🗑️ 撕便条 | `rm old.txt` |
| 9 | `curl 网址` | 发一个网络请求 | 📞 打电话给网址 | `curl https://baidu.com` |
| 10 | `help 命令` | 查看命令怎么用 | 📕 翻说明书 | `help cd` |

---

## 🔥 高频组合技（后续会用到）

```bash
# 看日志的最后20行
tail -20 /var/log/hermes.log

# 看哪些端口在被占用
netstat -tlnp

# 查某个进程还在不在
ps aux | grep hermes

# 给文件授权（让脚本可以执行）
chmod +x install.sh

# 后台运行一个服务
nohup ./start.sh &
```

---

## ⚡ Windows PowerShell 特别提醒

| 问题 | 解决 |
|:---|:---|
| `ls` 不识别？ | 用 `dir` 或 `Get-ChildItem` |
| `cat` 不识别？ | 用 `type` 或 `Get-Content` |
| `rm` 不识别？ | 用 `del` 或 `Remove-Item` |
| curl 返回一堆乱码？ | 用 `curl.exe` 而不是 `curl`（PowerShell的curl是别名） |

---

*创建日期：2026-06-21 | 手写一份效果更好*
