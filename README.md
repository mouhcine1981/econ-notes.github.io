# Your Economics Site

A GitHub Pages site built for publishing economic updates and analysis to
practitioners, policymakers, and researchers. No coding required for
day-to-day use — you're editing plain text files with a simple format.

---

## 1. First-time setup (do this once)

**A note on your repo name.** This site is configured for a repository
named **`econ-notes`** (a project site), which means your live URL will be
`https://yourusername.github.io/econ-notes/` — with `/econ-notes/` in the
path. If you ever rename the repo, update `baseurl` in `_config.yml` to
match (see step 4 below), or if you switch to a repo named exactly
`yourusername.github.io`, set `baseurl: ""` instead.

**Step 1 — Create the repository.**
On GitHub, create a new repository named `econ-notes` (or whatever you
actually chose — just make sure `baseurl` in `_config.yml` matches it,
prefixed with a `/`).

**Step 2 — Upload these files.**
Upload every file and folder in this project to that repository, keeping
the folder structure exactly as-is (the underscored folders — `_layouts`,
`_includes`, `_posts` — must stay named exactly that way; Jekyll looks for
them by name). The easiest way if you're not using git on the command line:
on the repo's GitHub page, use **Add file → Upload files** and drag the
whole folder in, or use GitHub Desktop (recommended — the browser uploader
sometimes flattens or skips these underscored folders).

**Step 3 — Turn on GitHub Pages.**
In the repository, go to **Settings → Pages**. Under "Build and deployment,"
set Source to **Deploy from a branch**, branch **main**, folder **/ (root)**.
Save. Give it 1-2 minutes, then visit
`https://yourusername.github.io/econ-notes/` (note the trailing slash and
the `/econ-notes/` path — bookmark this exact URL).

**Step 4 — Personalize `_config.yml`.**
Open `_config.yml` and replace the placeholder values:
- `title` — your name or site name
- `tagline` — the short eyebrow line (e.g., "Economic Research & Policy Notes")
- `description` — one sentence describing the site
- `url` — `https://yourusername.github.io` (your actual GitHub Pages domain, no path)
- `baseurl` — `/econ-notes` (already set correctly if you kept this repo name)
- `author: name` and `author: email` — your real name and contact email

Commit the change. The live site rebuilds automatically within a minute or two
every time you save a change to any file in the repo — there is no separate
"publish" button or build step to run yourself.

**Step 5 — Fill in About, Research, and Contact.**
Open `about.md`, `research.md`, and `contact.md`. Each has bracketed notes
in *italics* telling you exactly what to replace. Delete the italic notes
once you've written your real content.

**Step 6 — Delete or replace the 3 example posts.**
The `_posts/` folder has 3 example posts so you can see the design working.
Delete them once you have real posts, or leave one as a style reference —
your call.

---

## 2. Adding a new post (this is the main thing you'll do regularly)

1. In the `_posts/` folder, create a new file named exactly:
   `YYYY-MM-DD-a-short-slug.md`
   The date **must** be in that format and matches the publish date. The
   slug (the part after the date) can be anything — lowercase, words
   separated by hyphens, no spaces.

   Example: `2026-08-15-jobs-report-first-look.md`

2. Paste this at the very top of the file, exactly as shown, then fill in
   your own title, tags, and excerpt:

   ```
   ---
   title: "Your Post Title Here"
   tags: [inflation, labor-market]
   excerpt: "One or two sentences that show up in the list on the home page."
   ---
   ```

3. Below the `---`, write your post in plain Markdown:
   - `## Heading` for a section heading
   - `**bold**` and `*italic*`
   - `> ` at the start of a line for a pull-quote (styled distinctly on this site)
   - Standard Markdown tables and links work too

4. Save/commit the file. It appears on the home page automatically, newest
   first — you don't need to edit any other file or list it anywhere.

---

## 3. Adding a publication to the Research page

Open `research.md` and copy one of the existing `<li class="pub-item">` blocks,
edit the year, title, venue, and link, and paste it at the top of the list
(newest first).

---

## 4. Checking that a change actually deployed correctly

After any change, go to the **Actions** tab on your GitHub repository. You'll
see a "pages build and deployment" run — a green checkmark means it deployed
successfully; a red X means something broke (click into it to see the error,
usually a typo in a file's front matter — the three dashes and fields at
the very top of a post or page file). If you're ever unsure whether a change
went live, that Actions tab is the source of truth.

---

## 5. Adding a custom domain later (optional)

If you want `yourname.com` instead of `yourusername.github.io/econ-notes/`:
1. Buy the domain from any registrar (Namecheap, Google Domains successor,
   Cloudflare, etc. — roughly $10-15/year).
2. In the repo, go to **Settings → Pages → Custom domain**, enter your
   domain, and save. GitHub will show you the DNS records to add.
3. Add those DNS records at your registrar. This can take up to 24-48 hours
   to fully propagate, though it's often much faster.
4. **Important:** a custom domain serves your site at the root (no
   `/econ-notes/` path), so update `_config.yml`: set `baseurl: ""` (empty)
   and `url` to your new domain, e.g. `https://yourname.com`. Without this
   change, all your internal links will still point to the old
   `/econ-notes/...` paths and break.

This costs only the registrar's domain fee — GitHub Pages hosting itself
stays free either way.

---

## 6. Design reference

- Colors, fonts, and spacing all live in `assets/css/main.css`, with named
  values at the very top of the file (`--paper`, `--ink`, `--treasury`,
  `--ochre`, `--slate`, `--rule`) if you ever want to adjust the palette.
- Fonts are loaded from Google Fonts in `_includes/head.html`: Spectral
  (headlines), IBM Plex Sans (body), IBM Plex Mono (dates/tags/labels).
