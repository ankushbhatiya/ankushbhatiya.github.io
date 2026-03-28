# Global Alpha Engine Blog

A GitHub Pages blog for the Multi-Agent Hedge Fund project.

## 🚀 Quick Setup

### 1. Create a New Repository

1. Go to GitHub and create a new repository named `your-username.github.io`
   - Replace `your-username` with your actual GitHub username
   - Make it public
   - Don't initialize with README (we'll push this one)

### 2. Push This Blog to GitHub

```bash
# Navigate to the blog directory
cd github_blog

# Initialize git
git init

# Add all files
git add .

# Commit
git commit -m "Initial blog setup"

# Add your GitHub repo as remote
git remote add origin https://github.com/ankushbhatiya/ankushbhatiya.github.io.git

# Push to GitHub
git push -u origin main
```

### 3. Enable GitHub Pages

1. Go to your repository on GitHub
2. Click **Settings** → **Pages**
3. Under "Source", select **Deploy from a branch**
4. Select **main** branch and **/(root)** folder
5. Click **Save**

Your blog will be live at: `https://ankushbhatiya.github.io`

*(It may take 2-5 minutes to build and deploy)*

---

## ✏️ Customization

### Update Configuration

Edit `_config.yml`:

```yaml
title: "Your Blog Title"
description: "Your blog description"
author:
  name: "Your Name"
  email: "your.email@example.com"
github_username: your-github-username
twitter_username: your-twitter-handle
```

### Update GitHub Links

Replace all instances of `your-repo/hedge-fund` and `your-username` in:
- `_config.yml`
- `index.md`
- `_posts/2025-03-28-multi-agent-hedge-fund.md`
- `about.md`

### Add New Posts

1. Create a new file in `_posts/` with format: `YYYY-MM-DD-title.md`
2. Add front matter:
   ```yaml
   ---
   layout: post
   title: "Your Post Title"
   date: 2025-03-28 10:00:00 +0000
   categories: [category1, category2]
   tags: [tag1, tag2]
   ---
   ```
3. Write your content in Markdown

### Add Images

Place images in `assets/images/` and reference them:

```markdown
![Alt text](/assets/images/your-image.png)
```

---

## 🎨 Theme Customization

This blog uses the **minima** theme (GitHub Pages default). To change themes:

### Option 1: Use a Different GitHub Pages Theme

Edit `_config.yml`:

```yaml
theme: jekyll-theme-cayman  # or any supported theme
```

[Supported themes](https://pages.github.com/themes/)

### Option 2: Use a Custom Theme

1. Remove `theme: minima` from `_config.yml`
2. Add your theme's files to the repository

---

## 📝 Writing Posts

### Markdown Syntax

```markdown
# Heading 1
## Heading 2

**Bold text**
*Italic text*

- Bullet point
- Another point

1. Numbered list
2. Second item

[Link text](https://example.com)

![Image alt](/assets/images/image.png)

`inline code`

```python
# Code block
print("Hello World")
```
```

### Front Matter Options

```yaml
---
layout: post
title: "Post Title"
date: 2025-03-28 10:00:00 +0000
categories: [trading, python]
tags: [algo-trading, ai]
author: "Your Name"
excerpt: "Short description for previews"
image: /assets/images/hero.png
published: true  # or false for drafts
---
```

---

## 🔧 Local Development

To preview changes locally before pushing:

```bash
# Install Jekyll
gem install jekyll bundler

# Install dependencies
bundle install

# Serve locally
bundle exec jekyll serve

# Open browser to http://localhost:4000
```

---

## 📁 Directory Structure

```
github_blog/
├── _config.yml          # Site configuration
├── _posts/              # Blog posts
│   └── 2025-03-28-multi-agent-hedge-fund.md
├── _layouts/            # (optional) Custom layouts
├── assets/
│   └── images/
│       └── banner.svg
├── index.md             # Homepage
├── about.md             # About page
└── README.md            # This file
```

---

## 🔗 Useful Links

- [Jekyll Documentation](https://jekyllrb.com/docs/)
- [GitHub Pages Documentation](https://docs.github.com/en/pages)
- [Markdown Guide](https://www.markdownguide.org/)
- [Minima Theme](https://github.com/jekyll/minima)

---

## 🆘 Troubleshooting

### Changes not appearing?
- GitHub Pages takes 2-5 minutes to build
- Check **Settings** → **Pages** for build status
- Try hard refresh: `Ctrl+Shift+R` (or `Cmd+Shift+R` on Mac)

### Broken images?
- Ensure paths start with `/` (absolute)
- Check filename case sensitivity
- Verify images are in `assets/images/`

### Build failures?
- Check `_config.yml` for syntax errors
- Ensure no tabs in YAML (use spaces)
- Check GitHub email for build error details

---

## 📄 License

The blog content and code are released under the MIT License.
