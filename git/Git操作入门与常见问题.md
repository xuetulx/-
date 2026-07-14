# Git 操作入门与常见问题

> 来源：https://github.com/xuetulx/Study

Python 学习练习项目中的 Git 操作指南。

---

## 新仓库练习步骤

### 1. 在 GitHub 上创建仓库
- 在 GitHub 新建仓库，仓库名：`Study`
- 勾选"Add a README file"（自动生成初始提交）

### 2. 克隆仓库到本地
```bash
git clone https://github.com/xuetulx/Study.git
```

### 2.1 本地文件连接仓库提交推送
```bash
# 创建本地仓库
git init
# 连接远程服务器
git config --global user.name "你的git名"
git config --global user.name "你的邮箱（最好使用设置-电子邮件-保持我的电子邮件地址私密里的邮箱）"
git remote add origin 库的地址（打开要用的库在code-local-https复制）
```

### 3. 添加练习文件并提交
```bash
# 添加文件（main.py / lianxi.txt 等）
git add 文件夹名（文件夹内所有可提交的的文件都提交）
git add 文件名（提交单个文件）
git add .
git commit -m "feat(python):add 新建仓库练习用"
```

### 4. 处理远程与本地冲突（远端已有 Initial commit）
```bash
# 拉取远程代码并变基
git pull --rebase origin main
```

### 5. 推送到远程 main 分支
```bash
git push origin main
```

### 6. 创建新分支 `test` 并切换
```bash
# 创建并切换到 test 分支
git checkout -b test
```

### 7. 在 test 分支上修改并提交
```bash
# 创建 test.txt 并写入内容
git add test.txt
git commit -m "feat(txt):分支提交练习"
```

### 8. 切换回 main 分支
```bash
git checkout main
```

### 9. 将 test 分支合并到 main
```bash
git merge test
```

### 10. 推送到远程 main 分支
```bash
git push origin main
```

---

# 遇到的问题及解决方法

### 1. PowerShell 不支持 `&&` 连接多条命令

**问题：** 在 PowerShell 中使用 `&&` 连接多条命令时报错：
```
"&&"不是此版本中的有效语句分隔符
```

**解决方法：** PowerShell 应使用 `;`（分号）代替 `&&` 连接多条命令，或直接分条执行：
```powershell
cd "d:\4.python\练习1"; git status
```

> 注：Git Bash / Linux / macOS 终端可正常使用 `&&`

---

### 2. 本地与远程初始提交冲突

**问题：**
- 本地仓库先创建了提交 `feat(python):add 新建仓库练习用`（含 main.py）
- 但 GitHub 远端仓库创建时勾选了"Add a README"，已有一个 `Initial commit`
- 直接 `git push` 被拒绝，因为远程有本地没有的提交

**解决方法：** 使用 `git pull --rebase` 将远程的 `Initial commit` 拉到本地，并将本地提交变基到其上：
```bash
git pull --rebase origin main
```
这样本地提交就会排在远程 `Initial commit` 之后，历史保持线性整洁。

---

### 3. PowerShell 中没有 `head` 命令

**问题：** 尝试在 PowerShell 中使用管道 `| head -30` 报错：
```
无法将"head"识别为 cmdlet、函数、脚本文件或可运行程序的名称
```

**解决方法：** PowerShell 下使用 `Select-Object` 命令：
```powershell
# PowerShell 实现类似 head 的功能
git log --oneline | Select-Object -First 30
```
或切换到 Git Bash / WSL 终端执行。

---

## 常用 Git 命令速查

| 命令 | 说明 |
|------|------|
| `git clone <url>` | 克隆远程仓库 |
| `git add <file>` | 暂存文件 |
| `git commit -m "message"` | 提交暂存区 |
| `git push origin main` | 推送到远程 main |
| `git pull --rebase origin main` | 拉取远程并变基 |
| `git branch <name>` | 创建分支 |
| `git checkout -b <name>` | 创建并切换分支 |
| `git checkout <name>` | 切换分支 |
| `git merge <branch>` | 合并分支 |
| `git log --oneline --graph` | 查看提交历史 |
| `git status` | 查看工作区状态 |
