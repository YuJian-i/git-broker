# git-broker

GitHub Actions 云端 Git 历史打包服务。用于快速拉取任意 GitHub 公开仓库的完整 git 历史。

## 使用方法

1. 推送此仓库到 GitHub
2. 进入 Actions 页面，运行 "Git Bundle Export" workflow
3. 输入目标仓库（如 `astral-sh/uv`）
4. 等待 bundle 生成（通常 1-3 分钟）
5. 下载 artifact
6. 本地从 bundle 恢复：

```bash
# 从 bundle 创建 bare mirror
git clone --bare repo.bundle uv.git

# 或创建完整工作副本
git clone repo.bundle uv

# 审计验证
git -C uv.git fsck --full
git -C uv.git count-objects -vH
```

## 参数

- `repo`: 目标仓库，格式 `owner/name`
- `mode`: `bare`（默认，仅分支+标签）或 `mirror`（全部 ref 含 PR）
- `branch`: 指定分支，留空则为默认分支
