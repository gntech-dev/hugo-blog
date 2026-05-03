# hugo-blog

Static blog for GnTech, managed by Zeno 🤖, built with Hugo + PaperMod, and deployed via Cloudflare Pages at https://blog.gntech.me/

---

## 📚 What is this?
This is a static site (blog) powered by [Hugo](https://gohugo.io/) and the [PaperMod theme](https://github.com/adityatelange/hugo-PaperMod). All content and changes are managed via Git + GitHub, with fully automated deploys using [Cloudflare Pages](https://pages.cloudflare.com/).

- **Live Site:** [https://blog.gntech.me/](https://blog.gntech.me/)

---

## 🚀 Quickstart
1. **Edit or create posts:**
   - Blog posts live in `content/posts`. Each post is a Markdown file (`.md`).
   - To create a new post: add a `.md` file with proper front matter, or (locally) `hugo new posts/my-title.md`
2. **Commit and push:**
   - `git add . && git commit -m "Your message" && git push origin main`
3. **Deploy:**
   - Cloudflare Pages will auto-build & publish your changes when you push to `main`. Hugo works serverlessly—no need for hugo on the server.

---

## 🎨 Config (Site Settings & Theme)
- Main site config: [`hugo.toml`](./hugo.toml)
  - Site URL is set to `https://blog.gntech.me/` for correct navigation.
  - Change site title, baseURL, language, etc.
- Theme settings for [PaperMod](https://github.com/adityatelange/hugo-PaperMod#readme):
  - Located in `hugo.toml` under `[params]` section (add this if missing)
  - See the [PaperMod config docs](https://adityatelange.github.io/hugo-PaperMod/posts/papermod/papermod-configuration/) for available options

---

## ✍️ Writing Content
- **Posts:**  Place new Markdown files in `content/posts/` with front matter:
  ```markdown
  ---
  title: "My First Post"
  date: 2026-05-02T22:40:00-04:00
  draft: false
  ---

  Your content here.
  ```
- **Pages:** Place in `content/` or a `content/page/` folder. (e.g. About, Contact)
- Images/assets: Place under the `static/` directory for direct linking (e.g. `/img/foo.jpg`)

---

## 🛠️ Local development (optional)
If developing on your own machine (optional, needs Hugo):
```sh
hugo server -D
```
Access at [http://localhost:1313](http://localhost:1313)

---

## ⚡ Deployment to Cloudflare Pages
- Build command: `hugo`
- Output/public directory: `public`
- Hugo version specified in `.hugover`
- All settings managed in `.cfpages.toml`—auto-detect for Pages deploys.
- No wrangler/Workers files needed.
- See Cloudflare dashboard to manage domain & custom routing.

## Environment/Secrets (required for some automations)
In repo > Settings > Secrets & Variables > Actions:
- `CF_API_TOKEN`: [How to Create](https://developers.cloudflare.com/api/keys/create-token/): Pages Write permissions, scoped to your account/project.
- `CF_ACCOUNT_ID`: Find in Cloudflare dashboard under profile/account.
- `CF_PROJECT_NAME`: The project name in Cloudflare Pages (ex: hugo-blog)

---

## 🧩 Advanced (Theme updates, Custom builds)
- `git submodule update --remote --merge` (update themes)
- Customize theme under `themes/PaperMod/` or override in your own folders

---

## 🛑 Troubleshooting
- **Links go to wrong domain:** Check `baseURL` in `hugo.toml` matches your live domain.
- **404 or theme errors:** Ensure `theme = "PaperMod"` and run `git submodule update --init`.
- **Automatic build failed:** Make sure build command is `hugo` and not wrangler/Node.

## 📖 Resources
- [Hugo Documentation](https://gohugo.io/documentation/)
- [PaperMod Docs & Config](https://adityatelange.github.io/hugo-PaperMod/posts/papermod/papermod-configuration/)
- [Cloudflare Pages Docs](https://developers.cloudflare.com/pages/)

---

## 🤖 Maintained by Zeno (AI assistant)
Need changes, posts, automations, config tweaks? Just ask Zeno 🤖
