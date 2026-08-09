# DEPLOY.md — Agent-executable deployment guide

This guide is written so an AI coding agent can execute it top to bottom with no human input.
Every command is literal and copy-pasteable. Run them from the repository root unless stated otherwise.

**Artifact:** one static file, `docs/index.html`. No build step, no dependencies, no runtime.

---

## 0. Preconditions

```bash
gh auth status          # must show a logged-in account with 'repo' and 'workflow' scopes
git --version
```

If `gh auth status` fails, stop and instruct the human to run `gh auth login`. Do not attempt to
authenticate non-interactively.

Set the target once so every later command reuses it:

```bash
export GH_OWNER=wasay-09
export GH_REPO=ai-automation-studio
```

---

## 1. Primary path — GitHub Pages (recommended, free, zero config)

### 1.1 Create the repository and push

```bash
cd /path/to/ai-automation-studio
git init -b main                         # skip if already a repo
git add -A
git commit -m "Portfolio hub: five AI automation case studies"

gh repo create "$GH_OWNER/$GH_REPO" \
  --public \
  --source=. \
  --remote=origin \
  --push \
  --description "AI automation engineering portfolio — five live, clickable systems"
```

### 1.2 Enable Pages from the /docs folder

```bash
gh api -X POST "repos/$GH_OWNER/$GH_REPO/pages" \
  -f "source[branch]=main" \
  -f "source[path]=/docs"
```

A `409 Conflict` means Pages is already enabled — that is success, continue.

### 1.3 Verify

```bash
gh api "repos/$GH_OWNER/$GH_REPO/pages" --jq '.html_url, .status'
```

The first build takes 30–90 seconds. Poll until it returns HTTP 200:

```bash
URL=$(gh api "repos/$GH_OWNER/$GH_REPO/pages" --jq .html_url)
for i in $(seq 1 20); do
  CODE=$(curl -s -o /dev/null -w '%{http_code}' "$URL")
  echo "attempt $i: $CODE"
  [ "$CODE" = "200" ] && break
  sleep 15
done
curl -s "$URL" | grep -c "AI automations that" || echo "WARN: expected hero copy not found"
```

### 1.4 Add discoverability metadata

```bash
gh repo edit "$GH_OWNER/$GH_REPO" \
  --homepage "https://$GH_OWNER.github.io/$GH_REPO/" \
  --add-topic ai-automation \
  --add-topic portfolio \
  --add-topic freelance \
  --add-topic claude \
  --add-topic rag
```

---

## 2. Custom domain (optional but worth doing)

A custom domain raises reply rates on outbound noticeably. Two steps:

```bash
echo "automation.yourdomain.com" > docs/CNAME
git add docs/CNAME && git commit -m "Add custom domain" && git push
```

Then create this DNS record at the registrar:

| Type | Name | Value |
|---|---|---|
| CNAME | `automation` | `wasay-09.github.io` |

For an apex domain (`yourdomain.com`) use four A records instead: `185.199.108.153`,
`185.199.109.153`, `185.199.110.153`, `185.199.111.153`.

Then enforce HTTPS (wait for the certificate to provision first, usually under 15 minutes):

```bash
gh api -X PUT "repos/$GH_OWNER/$GH_REPO/pages" -F "https_enforced=true"
```

---

## 3. Alternative hosts

All of these serve the same `docs/` directory. Pick one; do not run several.

### 3.1 Cloudflare Pages

```bash
npm install -g wrangler
wrangler login                            # interactive — requires a human once
wrangler pages project create ai-automation-studio --production-branch main
wrangler pages deploy docs --project-name ai-automation-studio
```

### 3.2 Netlify

```bash
npm install -g netlify-cli
netlify login                             # interactive once
netlify deploy --dir=docs --prod
```

### 3.3 Vercel

```bash
npm install -g vercel
vercel login                              # interactive once
vercel deploy docs --prod
```

### 3.4 Any static host / S3

```bash
aws s3 sync docs/ "s3://your-bucket/" --delete --cache-control "public,max-age=300"
```

---

## 4. Post-deploy checklist

Run each and confirm before declaring the deploy done:

```bash
URL="https://$GH_OWNER.github.io/$GH_REPO/"

# 1. Page is live
curl -s -o /dev/null -w 'status=%{http_code}\n' "$URL"

# 2. No external network dependencies leaked in (must print 0)
grep -c -E 'src="https?://|href="https?://[^"]*\.css' docs/index.html

# 3. Every outbound demo link resolves
for p in leadflow-ai concierge-agent docuflow outreach-engine contentforge; do
  printf '%-20s ' "$p"
  curl -s -o /dev/null -w '%{http_code}\n' "https://$GH_OWNER.github.io/$p/"
done
```

Then check by eye, at 375px and 1440px widths:

- [ ] Hero renders, availability pulse animates
- [ ] All five "Open live demo" buttons open working demos
- [ ] "Copy email address" button copies and shows confirmation
- [ ] FAQ accordions open and close
- [ ] Nothing scrolls horizontally on mobile

---

## 5. Updating content

```bash
# edit docs/index.html
git add docs/index.html
git commit -m "Update <what changed>"
git push
# Pages rebuilds automatically in ~40s
```

Cache note: GitHub Pages sends a short `max-age`, but hard-refresh (`Cmd+Shift+R`) when verifying so
you aren't reading a stale copy.

---

## 6. Rollback

```bash
git log --oneline -10
git revert <bad-sha>          # preferred — keeps history honest
git push
```

Emergency full rollback to a known-good commit:

```bash
git reset --hard <good-sha>
git push --force-with-lease
```

To take the site offline entirely:

```bash
gh api -X DELETE "repos/$GH_OWNER/$GH_REPO/pages"
```

---

## 7. Troubleshooting

| Symptom | Cause | Fix |
|---|---|---|
| 404 after enabling Pages | Build not finished, or wrong source path | `gh api repos/$GH_OWNER/$GH_REPO/pages --jq .source` — must be `/docs` on `main` |
| Old content served | CDN cache | Hard refresh; confirm the commit actually pushed with `git log origin/main -1` |
| `409` on the Pages POST | Already enabled | Not an error — continue |
| `HTTP 403` from `gh api` | Token missing `repo` scope | `gh auth refresh -h github.com -s repo,workflow` |
| Demo links 404 | Sibling project not deployed yet | Deploy that project's own `DEPLOY.md`, then re-run the §4 link check |
