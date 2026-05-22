# Tangent Blog

Hugo-powered blog at [sixingwang2025.github.io/blog](https://sixingwang2025.github.io/blog/).

## Local Dev

```bash
hugo server
```

## Deploy

Build Hugo locally, then push — `public/` is committed to the repo. GitHub Actions deploys `./public` to the `gh-pages` branch and triggers the main site rebuild.

```bash
hugo --minify --baseURL "https://sixingwang2025.github.io/blog/"
git add public/ && git commit -m "update blog" && git push
```
