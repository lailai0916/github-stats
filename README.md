<div align="center">
  <h1>GitHub Stats Visualization</h1>
  <p><strong>English</strong> · <a href="README.zh-Hans.md">简体中文</a></p>
  <p>
    <img src="https://img.shields.io/github/actions/workflow/status/lailai0916/github-stats/main.yml?branch=master&style=flat-square" alt="CI" />
    <img src="https://img.shields.io/github/last-commit/lailai0916/github-stats?style=flat-square" alt="last commit" />
    <img src="https://img.shields.io/github/languages/top/lailai0916/github-stats?style=flat-square" alt="top language" />
    <img src="https://img.shields.io/github/repo-size/lailai0916/github-stats?style=flat-square" alt="repo size" />
    <img src="https://img.shields.io/github/license/lailai0916/github-stats?style=flat-square" alt="license" />
  </p>
</div>

## Project Introduction

Generate visualizations of GitHub user and repository statistics with GitHub Actions. The
visualizations can include private repositories and repositories you have contributed to without
owning. Generated images switch between GitHub light and dark themes automatically.

The project collects profile and repository statistics through the GitHub API, then writes SVG
images that can be embedded in a repository README or a profile README. It runs on GitHub Actions,
so no separate server is needed for scheduled regeneration.

## Project Features

📊 **Profile-aware statistics** — Include contributions and private-repository data that ordinary
public profile counters cannot represent.

⚙️ **Scheduled generation** — GitHub Actions regenerates the SVG visualizations without a separate
server or deployment.

🌗 **Theme-aware output** — Generated overview and language images provide separate light and dark
variants for GitHub's current color scheme.

🔐 **Configurable scope** — Exclude repositories or languages, and optionally exclude contributed
forks through repository secrets and workflow settings.

## Getting Started

Create a personal access token with `read:user` and `repo` permissions, then add it to the
repository's Actions secrets as `ACCESS_TOKEN`. The default GitHub Actions token is not sufficient
for private-repository statistics.

Configure optional `EXCLUDED` and `EXCLUDED_LANGS` secrets when needed. To exclude contributed
forks, set `EXCLUDE_FORKED_REPOS=true` in [`.github/workflows/main.yml`](.github/workflows/main.yml).

Run the [Generate Stats Images workflow](https://github.com/lailai0916/github-stats/actions/workflows/main.yml)
manually the first time. The generated files are written to [`generated/`](generated).

Embed the resulting images in another README with the repository's `master` branch:

```md
![](https://raw.githubusercontent.com/lailai0916/github-stats/master/generated/overview.svg#gh-dark-mode-only)
![](https://raw.githubusercontent.com/lailai0916/github-stats/master/generated/overview.svg#gh-light-mode-only)
![](https://raw.githubusercontent.com/lailai0916/github-stats/master/generated/languages.svg#gh-dark-mode-only)
![](https://raw.githubusercontent.com/lailai0916/github-stats/master/generated/languages.svg#gh-light-mode-only)
```

If the token can read private repositories, review workflow logs carefully: errors from API clients
can expose private repository names.

## Project Structure

```bash
github-stats/
├── .github/                        # GitHub configuration
│   └── workflows/                  # Automated workflows
│       └── main.yml                # Scheduled image generation
├── generated/                      # Generated overview and language images
├── templates/                      # SVG templates
├── generate_images.py              # Image generation entry point
├── github_stats.py                 # GitHub API and statistics logic
└── requirements.txt                # Python dependencies
```

## Disclaimer

GitHub's statistics API can return inaccurate view counts and line-change totals while its caches
are being refreshed. Contributions older than a year may also be omitted by the API. See the
upstream discussions in [issue #2](https://github.com/jstrieb/github-stats/issues/2),
[#3](https://github.com/jstrieb/github-stats/issues/3), and
[#13](https://github.com/jstrieb/github-stats/issues/13) for known limitations.

## Related Projects

The project was inspired by [anuraghazra/github-readme-stats](https://github.com/anuraghazra/github-readme-stats)
and uses [GitHub Octicons](https://primer.style/octicons/).

## License

This project's code is licensed under [GNU General Public License v3.0](LICENSE).
