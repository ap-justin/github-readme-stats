# self-hosted github-readme-stats

fork of [anuraghazra/github-readme-stats](https://github.com/anuraghazra/github-readme-stats). public vercel instance kept 503'ing, so hosting own.

## deploy

1. vercel.com/new → import this repo
2. add env var `PAT_1` = github PAT (classic, scopes: `repo`, `read:user`)
   - create at github.com/settings/tokens
3. deploy → note the url

## widening scope to org contributions

by default the stats card shows only public personal contribs. to include private repos and org work:

### 1. PAT scopes

create a **classic** PAT (not fine-grained — broader org support) at github.com/settings/tokens with:

- `repo` — full private repo access (needed for private contrib counts)
- `read:user` — profile data
- `read:org` — org membership + private org repos

set as `PAT_1` env var on vercel. re-deploy.

### 2. per-org settings (each org you contribute to)

go to `github.com/orgs/<ORG>/settings`:

- **Third-party Access → Personal access tokens**
  - if org has "Restrict access via fine-grained personal access tokens" enabled, your classic PAT may be blocked. either:
    - allow classic PATs (Personal access tokens (classic) → allow access via classic tokens), or
    - approve your specific token if approval flow is on
- **Member privileges → Repository visibility**: no change needed; PAT scope handles it
- if SSO/SAML is enforced: go to github.com/settings/tokens, find your PAT, click "Configure SSO" → authorize for each SAML org

### 3. profile setting (your own account)

github.com/settings/profile → check **"Include private contributions on my profile"**. without this, even with a privileged PAT, private commit counts won't appear on the contribution graph (the GRS api respects this flag).

### 4. card params

add to the stats card url:

- `count_private=true` — counts private contribs
- `include_all_commits=true` — lifetime, not just last year
- `include_orgs=true` (on some forks; original GRS auto-includes orgs once PAT can see them)

## wire to profile readme

update `ap-justin/ap-justin` README with your deploy url.

## refs

- upstream docs: https://github.com/anuraghazra/github-readme-stats#readme
- query params: theme, hide_border, bg_color, include_all_commits, count_private, layout, rank_icon, show, etc.
