# 📅 Day 4：Git 本地文件推送远程仓库完整指南

> **日期**：2026年6月21日（周日）
> **状态**：✅ 已完成
> **核心产出**：Git 推送操作文档 + Mermaid 流程图

---

## 🎯 核心流程图（总览）

```mermaid
flowchart TD
    A[本地项目文件夹] --> B{是否已初始化<br/>Git 仓库?}
    B -->|否| C[git init<br/>初始化仓库]
    B -->|是| D{是否已关联<br/>远程仓库?}
    C --> D
    D -->|否| E[git remote add origin<br/>关联远程仓库]
    D -->|是| F[git add .<br/>添加文件到暂存区]
    E --> F
    F --> G[git commit -m<br/>提交至本地仓库]
    G --> H{首次推送?}
    H -->|是| I[git push -u origin main<br/>推送并建立追踪关系]
    H -->|否| J[git push<br/>直接推送]
    I --> K[✅ 推送完成]
    J --> K

    style A fill:#e1f5fe
    style K fill:#c8e6c9
    style B fill:#fff9c4
    style D fill:#fff9c4
    style H fill:#fff9c4
```

---

## 📋 一、前置准备：初始化 Git 仓库

### 操作命令

```bash
# 1. 进入项目目录
cd 你的项目路径

# 2. 初始化 Git 仓库
git init

# 3. 查看仓库状态（验证是否成功）
git status
```

### 关键概念图解

```mermaid
flowchart LR
    subgraph 初始化前
        A[📁 项目文件夹] --> B[普通文件夹]
    end

    subgraph 初始化后
        C[📁 项目文件夹] --> D[.git 隐藏目录]
        D --> E[记录版本历史]
        D --> F[追踪文件变更]
        D --> G[配置信息]
    end

    初始化前 -.->|git init| 初始化后

    style 初始化前 fill:#ffccbc
    style 初始化后 fill:#c8e6c9
```

> 💡 `.git` 目录是 Git 的核心，存储了所有版本控制的元数据。删除 `.git` 目录就等于"解除"版本控制。

---

## 🔗 二、关联远程仓库

### 操作命令

```bash
# 方式1：HTTPS（推荐新手使用）
git remote add origin https://github.com/用户名/仓库名.git

# 方式2：SSH（需要先配置 SSH Key）
git remote add origin git@github.com:用户名/仓库名.git

# 查看已关联的远程仓库
git remote -v

# 如果填错了，先删除再重新添加
git remote remove origin
git remote add origin 新的地址
```

### 关系图解

```mermaid
flowchart TB
    subgraph 本地
        L[💻 本地仓库<br/>Local Repository]
    end

    subgraph 远程
        R[☁️ 远程仓库<br/>GitHub / GitLab / Gitee]
    end

    L <-.->|origin<br/>远程别名| R

    note1["`origin 是远程仓库的**别名**<br/>你可以改成任何名字<br/>但约定俗成都用 origin`"]

    R --- note1

    style L fill:#bbdefb
    style R fill:#c8e6c9
    style note1 fill:#fff9c4
```

---

## 📝 三、添加文件到暂存区

### 工作区 → 暂存区 → 本地仓库

```mermaid
flowchart LR
    A[📝 工作区<br/>Working Directory] -->|git add| B[📦 暂存区<br/>Staging Area]
    B -->|git commit| C[📚 本地仓库<br/>Local Repository]
    C -->|git push| D[☁️ 远程仓库<br/>Remote Repository]

    style A fill:#ffccbc
    style B fill:#fff9c4
    style C fill:#bbdefb
    style D fill:#c8e6c9
```

### 常用命令

```bash
# 添加所有文件
git add .

# 添加指定文件
git add index.html style.css

# 添加指定文件夹
git add src/

# 交互式添加（可以部分暂存）
git add -p

# 查看暂存区状态
git status
```

---

## 📦 四、提交到本地仓库

### 操作命令

```bash
# 提交并附上说明信息
git commit -m "feat: 初始化项目结构"

# 如果漏了文件，可以追加到上一次提交（不产生新提交记录）
git add 漏掉的文件
git commit --amend -m "feat: 初始化项目结构（补充）"
```

### 提交信息规范

```mermaid
flowchart LR
    A["feat: 新增功能"] --- B["fix: 修复 Bug"]
    B --- C["docs: 文档更新"]
    C --- D["style: 代码格式调整"]
    D --- E["refactor: 代码重构"]
    E --- F["test: 测试相关"]
    F --- G["chore: 构建/工具变动"]

    style A fill:#c8e6c9
    style B fill:#ffcdd2
    style C fill:#bbdefb
    style D fill:#fff9c4
    style E fill:#d1c4e9
    style F fill:#b2dfdb
    style G fill:#f0f4c3
```

> 📌 推荐格式：`类型: 简短描述`，如 `feat: 添加用户登录功能`

---

## 🚀 五、推送到远程仓库

### 完整推送流程

```mermaid
sequenceDiagram
    participant U as 👤 你
    participant L as 💻 本地仓库
    participant R as ☁️ 远程仓库

    U->>L: git add .
    Note over U,L: 将修改添加到暂存区

    U->>L: git commit -m "信息"
    Note over U,L: 提交到本地仓库

    U->>R: git push origin main
    Note over U,R: 推送至远程仓库

    R-->>U: ✅ 推送成功！
```

### 操作命令

```bash
# 首次推送（建立追踪关系）
git push -u origin main

# 后续推送（已绑定上游分支）
git push

# 强制推送（⚠️ 慎用！会覆盖远程历史）
git push --force
```

### 分支名对照

| 场景 | 分支名 |
|------|--------|
| GitHub 2020年后新建仓库 | `main` |
| GitHub 旧仓库 / GitLab | `master` |
| 查看当前分支 | `git branch` |

---

## ⚠️ 六、常见问题与解决

### 问题 1：远程仓库已有文件（如 README）

```mermaid
flowchart TD
    A[远程已有 README.md] --> B[git pull origin main<br/>--allow-unrelated-histories]
    B --> C{有冲突?}
    C -->|是| D[手动解决冲突<br/>→ git add → git commit]
    C -->|否| E[git push origin main]
    D --> E
    E --> F[✅ 解决]

    style A fill:#ffcdd2
    style F fill:#c8e6c9
```

```bash
# 解决方案
git pull origin main --allow-unrelated-histories
# 如果有冲突，手动解决后再：
git add .
git commit -m "merge: 合并远程 README"
git push origin main
```

### 问题 2：认证失败

| 方式 | 说明 |
|------|------|
| **HTTPS + Token** | 用 Personal Access Token 代替密码 |
| **SSH Key** | 一劳永逸，生成 `ssh-keygen` 后添加到 GitHub |
| **凭据缓存** | `git config --global credential.helper cache` |

### 问题 3：推送被拒绝（non-fast-forward）

```bash
# 先拉取远程最新代码
git pull origin main --rebase

# 解决冲突后再推送
git push origin main
```

---

## 🎯 极简速查表

```mermaid
flowchart TD
    S[开始] --> A["1️⃣ git init<br/>初始化仓库"]
    A --> B["2️⃣ git remote add origin URL<br/>关联远程"]
    B --> C["3️⃣ git add .<br/>添加文件"]
    C --> D["4️⃣ git commit -m 'msg'<br/>提交"]
    D --> E["5️⃣ git push -u origin main<br/>推送"]
    E --> F["🎉 完成！"]

    style S fill:#e1f5fe
    style F fill:#c8e6c9
```

| 步骤 | 命令 | 说明 |
|------|------|------|
| ① | `git init` | 初始化仓库（仅首次） |
| ② | `git remote add origin URL` | 关联远程（仅首次） |
| ③ | `git add .` | 添加到暂存区 |
| ④ | `git commit -m "信息"` | 提交到本地 |
| ⑤ | `git push -u origin main` | 推送到远程（首次用 -u） |

---

## 📌 补充：.gitignore 文件

在推送前，建议创建 `.gitignore` 忽略不需要版本控制的文件：

```gitignore
# 依赖
node_modules/
vendor/

# 环境文件
.env
.env.local

# 系统文件
.DS_Store
Thumbs.db

# IDE 配置
.idea/
.vscode/
*.swp
```

---

> 📝 **一句话总结**：`git init → git add → git commit → git push`，记住这四步就好！
