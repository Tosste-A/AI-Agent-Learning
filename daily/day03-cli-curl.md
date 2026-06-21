# 📅 Day 3：命令行生存技能 + curl第一次调用AI API

> **日期**：2026年6月24日（周三）
> **状态**：⏳ 待开始
> **核心产出**：命令速查表 + curl调用API成功截图

---

## 🎯 今日目标

| 任务 | 产出物 | 完成 |
|:---|:---|:---:|
| 掌握10个常用命令，手写速查表 | 命令速查表（手写/截图） | ⬜ |
| 用curl调用Kimi API，拿到JSON响应 | 终端截图（命令+响应高亮） | ⬜ |

> ⚠️ **关键控制点**：curl必须跑通，这是后续所有API测试的原子操作。

---

## 任务一：本地命令行生存技能

### 是什么？（用类比理解）

> 💻 **命令行 = 直接给电脑打字的指挥棒**
> - 图形界面（鼠标点点点）= 用手比划，不精确
> - 命令行（敲字）= 直接下指令，一个字不差
>
> 后续所有操作——SSH连服务器、看日志、查进程、调API——全部在命令行里完成。
> 学会10个命令，就像学会了"吃饭、走路、说话"这些生存技能。

### 具体动作（跟着做）

#### 第1步：打开终端

```
Windows：按 Win+R → 输入 powershell → 回车
Mac：    按 Cmd+空格 → 输入 terminal → 回车
```

#### 第2步：一个一个练下面10个命令

> 🔑 手动敲，不要复制粘贴！手指记忆很重要。

```powershell
# 1. pwd  —— 看看自己现在在哪个文件夹
pwd
# 你会看到类似：C:\Users\Administrator
# 含义：你现在站在这，就像GPS定位

# 2. ls   —— 看看当前文件夹里有什么
ls
# 你会看到当前目录下的文件和文件夹列表
# 含义：环顾四周，看看周围有什么

# 3. cd   —— 换个文件夹
cd Desktop
pwd          # 确认一下：你已经在桌面了
cd ..        # 回到上一级
pwd
# 含义：移动位置，"进房间"和"出房间"

# 4. mkdir —— 新建一个文件夹
mkdir test-folder
ls           # 看看建好了没
# 含义：建个新房间

# 5. echo  —— 输出一行字 / 创建一个文件
echo "hello world"
echo "这是今天的命令行练习" > test-folder/note.txt
# 含义：喊一嗓子 / 写便条

# 6. cat   —— 查看文件内容
cat test-folder/note.txt
# 含义：把便条读出来

# 7. rm    —— 删除文件
rm test-folder/note.txt
# ⚠️ 删了就没了！小心用
# 含义：撕掉便条扔垃圾桶

# 8. curl  —— 发网络请求（重点！）
curl https://www.baidu.com
# 你会看到一大堆HTML代码，这就是百度首页的"源代码"
# 含义：curl = 打个电话给一个网址，听它回什么

# 9. ps    —— 查看正在运行的程序（Windows用 tasklist）
tasklist | Select-Object -First 10
# 含义：看看电脑里现在有哪些程序在干活

# 10. help —— 不知道怎么用了？问帮助
help cd
help ls
# 含义：翻说明书
```

### 命令速查表（手写/打印）

| # | 命令 | 作用 | 类比 | 示例 |
|:---|:---|:---|:---|:---|
| 1 | `pwd` | 查看当前路径 | GPS定位 | `pwd` |
| 2 | `ls` / `dir` | 列出文件 | 环顾四周 | `ls` |
| 3 | `cd` | 切换目录 | 进房间/出房间 | `cd Desktop` / `cd ..` |
| 4 | `mkdir` | 新建文件夹 | 建新房间 | `mkdir test` |
| 5 | `echo` | 输出文字 | 喊一嗓子 | `echo "hello"` |
| 6 | `cat` / `type` | 查看文件内容 | 读便条 | `cat file.txt` |
| 7 | `rm` / `del` | 删除文件 | 撕掉便条 | `rm file.txt` |
| 8 | `curl` | 发HTTP请求 | 打电话给网址 | `curl https://xxx` |
| 9 | `ps` / `tasklist` | 查进程 | 看谁在干活 | `tasklist` |
| 10 | `help` / `man` | 查帮助 | 翻说明书 | `help cd` |

> 📝 **额外笔记**：Windows和Mac的命令略有不同，上面用 `/` 标注了。你用的是 Windows，记 PowerShell 版本即可。

### ✅ 检查点

- [ ] 10个命令都亲手敲过一遍
- [ ] 能手写出至少7个命令的作用（不查笔记）
- [ ] 已产出命令速查表（拍照或截图）

### 📸 截图区

> *粘贴：手写命令速查表的照片*

![命令速查表]()

---

## 任务二：curl实战 —— "第一次调用AI API"

### 是什么？（用类比理解）

> 🔌 **API = 程序的插座**
> - 你不需要知道"电"（模型）是怎么造的，你只需要把插头（请求）插进插座（API地址）
> - **curl = 测试这个插座有没有电的螺丝刀**
>
> 用curl调API，就像拿万用表测插座："喂，有电吗？" → 服务器回："有！这是你要的东西"

### 具体动作（跟着做）

#### 第1步：准备API Key

```
你的Kimi API Key 是：sk-________________________
（导师已提供，直接填到下面的命令里）
```

#### 第2步：执行curl命令

```powershell
# ⚠️ 把 YOUR_API_KEY 替换成你的真实Key
# 下面这个命令的意思是：
# "嘿，Kimi的API，我给你一句话（content），你帮我续写完成它（chat/completions）"

curl https://api.moonshot.cn/v1/chat/completions `
  -H "Content-Type: application/json" `
  -H "Authorization: Bearer YOUR_API_KEY" `
  -d '{`n  "model": "moonshot-v1-8k",`n  "messages": [`n    {"role": "user", "content": "用一句话解释什么是API"} `n  ]`n}'
```

> 💡 **PowerShell注意**：上面命令里的 `` `n `` 是PowerShell的换行符。如果报错，试试下面这个"一行版"：

```powershell
# 一行版（更不容易出错）
curl https://api.moonshot.cn/v1/chat/completions -H "Content-Type: application/json" -H "Authorization: Bearer YOUR_API_KEY" -d '{"model":"moonshot-v1-8k","messages":[{"role":"user","content":"用一句话解释什么是API"}]}'
```

#### 第3步：看懂返回的JSON

```json
// 成功的话，你会看到类似这样的东西：
{
  "id": "chatcmpl-xxxxx",
  "choices": [
    {
      "index": 0,
      "message": {
        "role": "assistant",
        "content": "API就像程序的插座，..."
      },
      "finish_reason": "stop"
    }
  ],
  "usage": {
    "prompt_tokens": 15,    // 你输入的token数
    "completion_tokens": 20, // 模型回复的token数
    "total_tokens": 35       // 总共消耗
  }
}
```

### 如果报错了怎么办？（3分钟自查流程）

| 报错信息 | 可能原因 | 解决 |
|:---|:---|:---|
| `401 Unauthorized` | API Key错了/过期了 | 检查Key是否正确复制 |
| `curl: command not found` | Windows没装curl | PowerShell一般自带，试试 `curl.exe` |
| `Could not resolve host` | 域名打错了 / 没联网 | 确认是 `api.moonshot.cn`，确认WiFi正常 |
| 返回一堆乱码 | PowerShell编码问题 | 正常，看有没有 `choices` 这个关键词 |

### ✅ 检查点

- [ ] curl命令执行成功，看到JSON响应
- [ ] 能在JSON里找到 `"choices"` → `"message"` → `"content"` 这个路径
- [ ] 理解了 `prompt_tokens` 和 `completion_tokens` 的区别
- [ ] 已截图保存（命令+返回结果）

### 📸 截图区

> *粘贴：终端截图，标注出以下位置：*
> - [ ] curl命令那一行
> - [ ] `"content"` 字段（模型的回答）
> - [ ] `"total_tokens"` 字段（消耗的token数）

![curl调用API截图]()

---

## 🧠 今日概念卡

| 概念 | 一句话 | 后续怎么用 |
|:---|:---|:---|
| **命令行** | 直接给电脑打字下指令 | SSH连服务器、查日志全靠它 |
| **curl** | 命令行里的"打电话"工具 | 验证API是否活着、后端服务是否正常 |
| **API** | 程序的插座，插上就能用 | Agent调模型、调工具都是通过API |
| **JSON** | 程序之间聊天的"通用语言"格式 | 看API响应、读日志、写测试用例都要看懂JSON |
| **token** | 模型"算账"的最小单位 | 理解模型怎么计费 |

---

## ❓ 今日疑问

| # | 问题 | 答案 |
|:---|:---|:---|
| 1 | | |
| 2 | | |

---

## 📝 今日小结

> *学习结束后写*

今日收获：

踩坑记录：

---

*下一站：Day 4 → Web工作原理实操（F12 Network）*
