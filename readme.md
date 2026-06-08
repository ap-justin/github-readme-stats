# self-hosted github-readme-stats

fork of [anuraghazra/github-readme-stats](https://github.com/anuraghazra/github-readme-stats). public vercel instance kept 503'ing, so hosting own.

## deploy

1. vercel.com/new → import this repo
2. add env var `PAT_1` = github PAT (classic, scopes: `repo`, `read:user`)
   - create at github.com/settings/tokens
3. deploy → note the url

## wire to profile readme

in `ap-justin/ap-justin` PR #2, replace `<YOUR-VERCEL-URL>` with the deploy url, then merge.

```
gh pr checkout 2 -R ap-justin/ap-justin
sed -i '' 's|<YOUR-VERCEL-URL>|<actual>.vercel.app|g' README.md
git commit -am "set vercel url" && git push
gh pr merge 2 -R ap-justin/ap-justin --squash
```

## refs

- upstream docs: https://github.com/anuraghazra/github-readme-stats#readme
- query params: theme, hide_border, bg_color, include_all_commits, count_private, layout, etc.
