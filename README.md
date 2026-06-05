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
`claude-agentic-qe` repo. **First** update the status at the source
(`/qa-test` runs regenerate module reports; `/qa-curate` regenerates the
Executive dashboard). **Then** publish with a single command from the main
repo root:

```bash
node scripts/publish-qa-site.mjs "Update QA status after SN-66 re-run"
```

That one command:
1. rebuilds `SproutNext_QA_Report_complete.html` (Executive + all 9 module tabs),
2. refreshes this folder (`index.html` + `modules/`),
3. commits and pushes → Vercel redeploys (~30s).

Pass `--no-push` to build + commit locally without publishing. If you only
changed files and want the copy step alone, `node scripts/build-qa-site.mjs`
still works on its own.
