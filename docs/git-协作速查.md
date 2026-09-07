# Git 协作速查

- 仓库：`https://github.com/Sol375/test01`（**Public，公开可见**）
- 本地工作目录：`D:\Program\process\2026-09-07-16-19-47\thesis-topic\`
- 默认分支：`main`

## 1. 每天开工前

```bash
git pull --rebase      # 先把别人的改动拉下来
```

## 2. 改完东西提交

```bash
git status                    # 看改了哪些文件
git add <具体文件>            # 别无脑 git add -A
git commit -m "说明：改了什么、为什么"
git push
```

**为什么必须先 pull**：同门可能已经 push 过，直接 push 会被拒绝（`non-fast-forward`）。

## 3. 遇到冲突怎么办

现象：
```
CONFLICT (content): Merge conflict in docs/outline.md
```
文件里会出现这种标记：
```
<<<<<<< HEAD
你的内容
=======
同门的内容
>>>>>>> 
```
处理：手动把内容改成正确的版本，**删掉 `<<<<<<<` `=======` `>>>>>>>` 三行标记**，然后：
```bash
git add docs/outline.md
git rebase --continue
```
想放弃这次合并、回到拉取前的状态：
```bash
git rebase --abort
```

## 4. 拉同门进来一起写

仓库网页 → Settings → Collaborators → Add people → 填对方 GitHub 用户名或邮箱 → 发邀请，对方接受后即可 push。
只想让人看不想让人改：给对方仓库链接即可（Public 仓库本来就可读）。

## 5. 公开仓库安全自查（push 前必做）

```bash
git status                              # 不应出现真实数据文件
git check-ignore -v data/raw/xxx.csv    # 有输出 = 已被忽略（安全）；无输出 = 危险，先别 push
```

仓库是公有的，**数据、授权代码、含个人信息的日志一律不能提交**。已在 `.gitignore` 中被挡掉的：
`data/raw/`、`data/processed/`、`*.csv *.xlsx *.parquet`、`*.pkl *.pt *.pth *.ckpt *.bin`、`logs/ outputs/`。

## 6. 出错回滚

```bash
git reflog                 # 找最近的安全提交
git reset --hard <commit号> # 回到那个状态（会丢弃工作区改动，慎用）
```
最差情况：整个目录删掉，从备份 `thesis-topic_backup_2026-09-07` 恢复，或重新 `git clone`。

## 7. 已知待办

- `.gitignore` 忽略了原始数据和模型权重，所以合作者 clone 下去**跑不了实验**。等人真的要一起跑时，再定数据共享方案（网盘 / Release 附件 / Git LFS / DVC 四选一）。
- 目前所有人直接往 `main` 上推。等人多起来，再考虑分支保护 + Pull Request 审查。
