# hugo-blog

Static blog for GnTech, managed by Zeno 🤖, built with Hugo + PaperMod, and deployed via Cloudflare Pages.

---

## 📚 What is this?
This is a static site (blog) powered by [Hugo](https://gohugo.io/) and the [PaperMod theme](https://github.com/adityatelange/hugo-PaperMod). All content and changes are managed via Git + GitHub, with fully automated deploys using [Cloudflare Pages](https://pages.cloudflare.com/).

---

## 🚀 Quickstart
1. **Edit or create posts:**
   - Blog posts live in `content/posts`. Each post is a Markdown file (`.md`).
   - To create a new post: `hugo new posts/my-title.md` (or copy/edit an old file)
2. **Commit and push:**
   - `git add . && git commit -m "Your message" && git push origin main`
3. **Deploy:**
   - Cloudflare Pages will auto-build & publish your changes when you push to `main`. No server-side hugo needed.

---

## 🎨 Config (Site Settings & Theme)
- Main site config: [`hugo.toml`](./hugo.toml)
  - Change site title, baseURL, language, etc.
- Theme settings for [PaperMod](https://github.com/adityatelange/hugo-PaperMod#readme):
  - Located in `hugo.toml` under `[params]` section (add this if missing)
  - See the [PaperMod config docs](https://adityatelange.github.io/hugo-PaperMod/posts/papermod/papermod-configuration/) for available options

---

## ✍️ Writing Content
- **Posts:**  Place new Markdown files in `content/posts/`. Example:
  ```markdown
  ---
  title: "My First Post"
  date: 2026-05-02
  draft: false
  ---

  Your content here.
  ```
- **Pages:** Place in `content/` or a `content/page/` folder. (e.g. About, Contact)
- Images/assets: Place under the `static/` directory for direct linking (e.g. `/img/foo.jpg`)

---

## 🛠️ Local development (optional)
If you want to preview the blog locally (requires Hugo):
```sh
hugo server -D
```
Access local site at [http://localhost:1313](http://localhost:1313)

---

## ⚡ Deployment to Cloudflare Pages
**Overview:** Pushing to `main` branch will trigger a deploy on Cloudflare Pages via the GitHub <-> Cloudflare integration or Actions.

### Build settings for Cloudflare Pages
> **Note:** This repo ships with a `.cfpages.toml` file that tells Cloudflare Pages exactly how to build & serve your site. All you have to do is link the repo in the Pages dashboard.

- **Build Command:** `hugo`
- **Output Directory:** `public`
- **Hugo Version:** Controlled by `.hugover` file (default: 0.121.2)

### Required Secrets
In your repo’s GitHub settings > Secrets and variables > Actions, set:
- `CF_API_TOKEN`: [How to Create](https://developers.cloudflare.com/api/keys/create-token/): Pages Write permissions, scoped to your account/project.
- `CF_ACCOUNT_ID`: Find in Cloudflare dashboard under your profile/account.
- `CF_PROJECT_NAME`: The project name you assign in Cloudflare Pages (usually `hugo-blog`)

**After first push:**
1. Visit Cloudflare Pages dashboard and create a new project, linking this GitHub repo.
2. Set environment variables as above in the Pages settings if needed.
3. Trigger a deploy by pushing a commit to main.

---

## 🧩 Advanced (Theme updates, Custom builds)
- **Update theme:**
  - `git submodule update --remote --merge`
- **Theme customizations:**
  - Update content in `themes/PaperMod/` or override styles in your own repo folders.

---

## 🛑 Troubleshooting
- **My site doesn’t update after push:** Check build logs on Cloudflare Pages dashboard.
- **404 or theme errors:** Verify `theme = "PaperMod"` is set in `hugo.toml`. Ensure submodules are cloned (`git submodule update --init`)
- **Local hugo errors:** Make sure local Hugo version matches/compatible with the theme’s requirements.

---

## 📖 Resources
- [Hugo Documentation](https://gohugo.io/documentation/)
- [PaperMod Docs & Config](https://adityatelange.github.io/hugo-PaperMod/posts/papermod/papermod-configuration/)
- [Cloudflare Pages Docs](https://developers.cloudflare.com/pages/)

---

## 🤖 Maintained by Zeno (AI assistant)
Need changes, new posts, or help? Talk to Zeno 🤖
