<div align="center">
  <h1>GitHub Stats Visualization</h1>
  <p><a href="README.md">English</a> · <strong>简体中文</strong></p>
  <p>
    <img src="https://img.shields.io/github/actions/workflow/status/lailai0916/github-stats/main.yml?branch=master&style=flat-square" alt="CI" />
    <img src="https://img.shields.io/github/last-commit/lailai0916/github-stats?style=flat-square" alt="最后提交" />
    <img src="https://img.shields.io/github/languages/top/lailai0916/github-stats?style=flat-square" alt="主要语言" />
    <img src="https://img.shields.io/github/repo-size/lailai0916/github-stats?style=flat-square" alt="仓库大小" />
    <img src="https://img.shields.io/github/license/lailai0916/github-stats?style=flat-square" alt="许可证" />
  </p>
</div>

## 项目简介

使用 GitHub Actions 生成 GitHub 用户与仓库统计图。统计范围可以包含私有仓库，以及参与贡献但并不拥有的仓库；生成的图片会根据 GitHub 当前配色自动切换浅色与深色版本。

项目通过 GitHub API 收集个人资料与仓库统计数据，再写出可以嵌入仓库 README 或个人主页 README 的 SVG 图片。整个流程运行在 GitHub Actions 上，不需要单独维护服务器。

## 项目特性

📊 **面向个人资料的统计** — 展示普通公开主页计数器无法完整表达的贡献与私有仓库数据。

⚙️ **定时生成** — 由 GitHub Actions 定时重新生成 SVG 图表，无需单独部署服务器。

🌗 **适配主题** — 概览图与语言图分别提供浅色和深色版本，匹配 GitHub 当前配色。

🔐 **可配置统计范围** — 可以通过仓库 Secrets 和工作流设置排除仓库、语言或参与贡献的 fork。

## 快速开始

创建具有 `read:user` 和 `repo` 权限的个人访问令牌，并将它保存为仓库 Actions Secret `ACCESS_TOKEN`。默认的 GitHub Actions token 不足以读取私有仓库统计数据。

需要时配置 `EXCLUDED` 和 `EXCLUDED_LANGS` Secrets。若要排除参与贡献的 fork，在
[`.github/workflows/main.yml`](.github/workflows/main.yml) 中设置 `EXCLUDE_FORKED_REPOS=true`。

首次使用时，手动运行 [Generate Stats Images 工作流](https://github.com/lailai0916/github-stats/actions/workflows/main.yml)。生成文件会写入 [`generated/`](generated)。

在其他 README 中引用 `master` 分支的图片：

```md
![](https://raw.githubusercontent.com/lailai0916/github-stats/master/generated/overview.svg#gh-dark-mode-only)
![](https://raw.githubusercontent.com/lailai0916/github-stats/master/generated/overview.svg#gh-light-mode-only)
![](https://raw.githubusercontent.com/lailai0916/github-stats/master/generated/languages.svg#gh-dark-mode-only)
![](https://raw.githubusercontent.com/lailai0916/github-stats/master/generated/languages.svg#gh-light-mode-only)
```

如果令牌可以读取私有仓库，请仔细检查工作流日志：API 客户端的错误信息可能暴露私有仓库名称。

## 项目结构

```bash
github-stats/
├── .github/                        # GitHub 配置
│   └── workflows/                  # 自动化工作流
│       └── main.yml                # 定时生成统计图片
├── generated/                      # 生成的概览图与语言图
├── templates/                      # SVG 模板
├── generate_images.py              # 图片生成入口
├── github_stats.py                 # GitHub API 与统计逻辑
└── requirements.txt                # Python 依赖
```

## 免责声明

GitHub 统计 API 在缓存刷新期间可能返回不准确的访问量和代码变更总量；超过一年没有贡献的仓库也可能因 API 限制而被忽略。已知限制可参见上游的 [issue #2](https://github.com/jstrieb/github-stats/issues/2)、[#3](https://github.com/jstrieb/github-stats/issues/3) 和 [#13](https://github.com/jstrieb/github-stats/issues/13)。

## 相关项目

本项目受到 [anuraghazra/github-readme-stats](https://github.com/anuraghazra/github-readme-stats) 启发，并使用 [GitHub Octicons](https://primer.style/octicons/)。

## 许可协议

本项目代码采用 [GNU General Public License v3.0](LICENSE)。
