# TrueSignal Blog — Setup Instructions

This guide gets the blog live at `truesignal.live/blog/` in about 10–15 minutes. Your existing homepage at `truesignal.live` is **completely unchanged** by this setup — Jekyll only processes files with YAML front-matter, so `index.html` (which has no front-matter) passes through untouched.

---

## What you're getting

- A blog index at `https://truesignal.live/blog/`
- Two posts:
  - **"Why TrueSignal Doesn't Know Where You Are"** — set to publish immediately
  - **"Why Your Bars Lie"** — set to `published: false` (held for the Android launch / Show HN moment)
- An RSS feed at `https://truesignal.live/blog/feed.xml`
- A sitemap at `https://truesignal.live/sitemap.xml` (helps Google index everything)
- Auto-generated SEO meta tags on every page
- Visual styling that matches your existing site (dark + green + Syne/DM Mono, with Inter for body copy because monospace is hard to read at length)
- A "Blog" link in your nav
- A "Get TrueSignal" CTA at the end of every post

---

## Step 1 — Drop these files into your repo

The files in this bundle should go into your `truesignal-landing` repo at these exact paths:

```
truesignal-landing/
├── _config.yml                                                  ← NEW
├── _layouts/
│   ├── default.html                                             ← NEW
│   ├── post.html                                                ← NEW
│   └── blog_index.html                                          ← NEW
├── _posts/
│   ├── 2026-04-26-why-truesignal-doesnt-know-where-you-are.md   ← NEW
│   └── 2026-05-01-why-your-bars-lie.md                          ← NEW (held)
├── blog/
│   └── index.html                                               ← NEW
├── assets/
│   └── css/
│       └── blog.css                                             ← NEW
├── index.html                                                   ← UNCHANGED
└── (everything else)                                            ← UNCHANGED
```

The folder names that start with an underscore (`_config.yml`, `_layouts`, `_posts`) are Jekyll conventions — don't rename them.

---

## Step 2 — Commit and push

```bash
git add _config.yml _layouts _posts blog assets/css
git commit -m "Add Jekyll blog setup with first two posts"
git push
```

GitHub Pages will detect the `_config.yml` and start building the site as Jekyll. The first build takes 1–2 minutes. You can watch the progress in your repo under **Actions** (or **Settings → Pages → Build & deployment**).

---

## Step 3 — Verify

Once GitHub Pages finishes building, check:

- [ ] `https://truesignal.live/` — homepage looks identical to before (you should see no visual change)
- [ ] `https://truesignal.live/blog/` — blog index loads, shows the privacy post (and only the privacy post — the Bars post is held)
- [ ] `https://truesignal.live/blog/why-truesignal-doesnt-know-where-you-are/` — the privacy post renders correctly
- [ ] Click "Blog" in the nav from the homepage — it works
- [ ] Click "TrueSignal" logo from a blog page — returns to homepage
- [ ] `https://truesignal.live/blog/feed.xml` — returns valid RSS XML
- [ ] `https://truesignal.live/sitemap.xml` — returns the sitemap

If anything looks broken, check the GitHub Actions tab in your repo — it'll show the build error message.

---

## Step 4 — Submit the sitemap to Google

Once the sitemap is live:

1. Go to [Google Search Console](https://search.google.com/search-console)
2. Add `truesignal.live` as a property if you haven't already
3. Under **Sitemaps**, submit `https://truesignal.live/sitemap.xml`

This tells Google your blog exists and to crawl it. SEO indexing usually starts within a day or two.

---

## How to publish a new post

1. Create a new file in `_posts/` with the filename format `YYYY-MM-DD-slug.md`. The date in the filename is what Jekyll uses to set the post date.

2. At the top of the file, include this front-matter:

```yaml
---
title: "Your Post Title Here"
description: "A 1-2 sentence summary that shows up in search results, RSS, and the blog index."
date: 2026-05-15
author: "Dave Schwind"
---
```

3. Write the post in markdown below the front-matter.

4. Commit and push. GitHub Pages will rebuild and the post will go live within ~1 minute.

### Holding a post for later (like the Bars post)

Add `published: false` to the front-matter:

```yaml
---
title: "..."
description: "..."
date: 2026-05-15
author: "Dave Schwind"
published: false
---
```

When you're ready to publish, change to `published: true` (or just delete that line) and push.

---

## How to publish the Bars post when Android launches

Edit `_posts/2026-05-01-why-your-bars-lie.md` and change the front-matter:

- Update the `date:` to the actual launch day (e.g. `2026-05-15`)
- Rename the file to match (`2026-05-15-why-your-bars-lie.md`)
- Remove the `published: false` line

Commit and push. The post goes live, the RSS feed updates, and the blog index will show it as the most recent post.

---

## Markdown quick reference

For when you write your own posts:

```markdown
## A section heading

A paragraph. Just write normally.

Another paragraph. Two paragraphs are separated by a blank line.

**Bold text** and *italic text*.

[A link to something](https://example.com)

A bulleted list:
- Item one
- Item two
- Item three

> A blockquote, for pulling out a key sentence.

`inline code` for technical terms.

---

A horizontal rule (three dashes on their own line) for major breaks.
```

That's enough for 95% of blog posts. The CSS handles all the styling — you just write content.

---

## Troubleshooting

**The site builds but the blog page is 404.**
Wait 2 more minutes. GitHub Pages sometimes takes longer to propagate the first time you add a new directory.

**The CSS isn't loading and the blog looks like raw text.**
Check that `assets/css/blog.css` is at the right path. Jekyll serves it from `/assets/css/blog.css` and the layouts reference it that way.

**A post isn't showing up on the blog index.**
Check the file is in `_posts/` (not `posts/`), the filename matches the `YYYY-MM-DD-slug.md` format, and the front-matter doesn't have `published: false`.

**The build is failing in GitHub Actions.**
Open the failing build in the Actions tab, scroll to the error message. 90% of the time it's a YAML front-matter syntax error — usually a smart quote where there should be a regular quote, or a missing closing quote on a `title:` or `description:`.

**The homepage broke.**
Shouldn't happen — `index.html` has no front-matter so Jekyll doesn't touch it. But if it does, just remove `_config.yml` and the site reverts to a non-Jekyll static site.

---

## What this setup does NOT include

To keep things simple and respectful of your audience, this setup deliberately omits:

- Analytics (Google Analytics, Plausible, etc.) — your readers are privacy-conscious
- Comments (Disqus, etc.) — high spam, low signal, and they slow page loads
- Social share buttons — your audience already knows how to copy a URL
- Newsletter signup — can be added later when there's enough traffic to make it worth managing
- Tags or categories — overkill at 1-2 posts/month; can be added later if needed

Everything in this list can be added incrementally as the blog grows.

---

## Questions / changes

If anything needs adjusting (visual tweaks, additional features, different layout), just say the word and we'll iterate.
