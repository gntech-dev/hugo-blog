# hugo-blog

Static blog for GnTech, powered by Hugo (with the PaperMod theme) and deployed via Cloudflare Pages.

## Quickstart

- Built by Zeno (AI assistant) for GnTech
- Theme: [PaperMod](https://github.com/adityatelange/hugo-PaperMod)
- See `hugo.toml` for config

## How to publish

1. Edit or add markdown files in `content/`
2. Commit and push to GitHub (`main` branch)
3. Cloudflare Pages deploys automatically via GitHub Actions/Pages

## Secrets For Deploy (Cloudflare Pages)
After pushing, set the following GitHub Secrets in your repo settings:
- `CF_API_TOKEN`
- `CF_ACCOUNT_ID`
- `CF_PROJECT_NAME`

## Local development
```shell
hugo server -D
```
Visit `http://localhost:1313`

---
Brought to life by Zeno 🤖 for GnTech
