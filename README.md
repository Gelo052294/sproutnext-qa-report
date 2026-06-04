# SproutNext QA Report — Live Site

Static site hosting the SproutNext QA status reports. Deployed on Vercel,
auto-redeploys on every push to `main`.

## URLs

| Page | Path |
|------|------|
| Full report (Executive + all modules) | `/` |
| Module index | `/modules` |
| A single module | `/modules/sn-66-workforce`, `/modules/sn-26-bulk-upload`, … |

## First-time deploy (GitHub + Vercel)

1. Create a new **empty** GitHub repo, e.g. `sproutnext-qa-report` (no README).
2. From this folder, push it up:
   ```bash
   git remote add origin https://github.com/<you>/sproutnext-qa-report.git
   git branch -M main
   git push -u origin main
   ```
3. Go to **vercel.com → Add New → Project**, import the repo.
   - Framework Preset: **Other**
   - Build Command: *(leave empty)*
   - Output Directory: *(leave empty — root is served as-is)*
4. Deploy. You get `https://sproutnext-qa-report.vercel.app`.

Every later `git push` to `main` triggers a fresh deploy automatically.

## Refreshing the report ("live update")

The HTML here is generated from the QA artifacts in the main
`claude-agentic-qe` repo. To publish updated results:

```bash
# in the main claude-agentic-qe repo
node scripts/build-qa-site.mjs      # regenerates qa-report-site/

# then in this folder
git add -A && git commit -m "Update QA report" && git push
```

Vercel rebuilds and the live URL reflects the new data within ~30s.
