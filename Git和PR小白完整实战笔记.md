# Git 和 PR 1 分钟速查版

## 1. 先死记这几句

- `commit`：本地保存一次代码版本
- `push`：把本地提交传到 GitHub
- `pull`：把远程最新代码拉到本地当前分支
- `branch`：你的开发分支
- `merge`：把一个分支并到另一个分支
- `PR`：请求把我的分支合并到目标分支

最重要的两句：

- `git merge X` = 把 `X` 合并到当前分支
- PR = 把我的分支请求合并进目标分支

---

## 2. 工作里最常用流程

```powershell
git checkout master
git pull
git checkout -b feature/xxx
git add .
git commit -m "feat: xxx"
git push -u origin feature/xxx
```

然后去 GitHub 提 PR。

---

## 3. 工作里最常见场景

### 新功能开发

```powershell
git checkout master
git pull
git checkout -b feature/login
```

意思：先基于最新主分支拉一个自己的分支，再开发。

### 提交代码

```powershell
git status
git add .
git commit -m "feat: add login"
```

意思：先确认改动，再提交。

### 推送分支

```powershell
git push -u origin feature/login
```

意思：把本地功能分支推到 GitHub。

### 创建 PR

GitHub 上通常选：

- `base: master`
- `compare: feature/login`

意思：把 `feature/login` 合并进 `master`。

### 同步主分支到你的功能分支

```powershell
git checkout master
git pull
git checkout feature/login
git merge master
```

意思：把最新主分支带进你的功能分支。

### `merge` 冲突

场景：你和别人改了不同分支里的同一块代码。

常见提示：

```text
CONFLICT (content): Merge conflict in xxx.py
```

意思：不同分支冲突了，要手动改文件。

### `pull` 冲突

场景：你本地当前分支改了，远程同名分支也改了同一块代码。

你执行：

```powershell
git pull
```

可能冲突。

意思：本地当前分支和远程当前分支冲突了。

### PR 合并后本地收尾

```powershell
git checkout master
git pull
git branch -d feature/login
```

意思：同步最新主分支，并删除已完成的本地分支。

---

## 4. 最容易混的两个点

### `git merge` 怎么记

只记：

**我站在哪个分支上，就是把别人并到这个分支里。**

例如：

```powershell
git checkout master
git merge feature/test
```

意思：把 `feature/test` 并进 `master`。

### `pull` 和 `merge` 区别

- `pull`：更新当前分支
- `merge`：手动把另一个分支并到当前分支

---

## 5. 最值得养成的习惯

- 每次提交前先 `git status`
- 每天开工前先 `git pull`
- 不要直接在 `master/main` 上写功能
- 一个功能一个分支
- 冲突时不要直接全保留自己代码
- PR merge 完后，本地记得 `git pull`

