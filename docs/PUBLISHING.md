# 提交与发布

## 发布前检查

在 PowerShell 中进入本项目：

```powershell
Set-Location -LiteralPath 'C:\Users\Joanna\Desktop\个人博客'
git status --short
git diff
git remote -v
```

检查姓名、简介、文章正文、项目链接和配色。`origin` 应为：

```text
https://github.com/xujiao77/xujiao77.github.io.git
```

`upstream` 保留原模板地址；发布时只推送到 `origin`。

## 确认后首次提交与推送

```powershell
git add .
git diff --cached --check
git diff --cached
git commit -m "Customize personal Jekyll blog"
git push -u origin main
```

首次推送会把原模板历史和本次修改一同发送到自己的仓库。上述提交与推送需在检查并确认后执行。

## 查看发布结果

```powershell
gh run list --repo xujiao77/xujiao77.github.io --workflow pages.yml --limit 5
```

在 [Actions 页面](https://github.com/xujiao77/xujiao77.github.io/actions) 中打开最新的 `Build and deploy Jekyll site` 记录。构建和部署均成功后，访问 <https://xujiao77.github.io/>。

如果发布来源尚未启用，在 [Pages 设置](https://github.com/xujiao77/xujiao77.github.io/settings/pages) 中把 Source 设为 **GitHub Actions**，然后在 Actions 页面重新运行工作流。这里只设置发布来源，不需要自建 Token 或添加仓库 Secret。

## 后续写作

文章写在 `_posts/YYYY-MM-DD-title.md`，保留 Front Matter 和 `layout: post`。文章日期不要写到未来，否则默认不会发布。文章与关于页的内部链接应使用 Jekyll 的 `relative_url` 或 `post_url`，资源放在 `assets/`。

修改后重复检查、提交和推送；对 `main` 的推送自动发布。Pull request 会构建检查，不部署网站。

本地直接双击 `index.html` 无法渲染 Liquid 模板与 Markdown。当前不安装本地 Jekyll，最终页面以 GitHub Actions 生成的结果为准。
