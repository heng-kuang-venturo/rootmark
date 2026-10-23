# Rootmarks.com — DNS & GitHub Pages setup

**Brand:** Rootmark  
**Domain:** [rootmarks.com](https://rootmarks.com)  
**Repo:** https://github.com/heng-kuang-venturo/rootmark  
**Pages source:** branch `main`, folder `/` (repo root)

## What Henry does at the registrar

Point DNS for `rootmarks.com` at GitHub Pages.

### Apex (`rootmarks.com`)

Add **four A records** (host `@` or blank, depending on registrar):

| Type | Name | Value |
|------|------|--------|
| A | `@` | `185.199.108.153` |
| A | `@` | `185.199.109.153` |
| A | `@` | `185.199.110.153` |
| A | `@` | `185.199.111.153` |

If the registrar supports **ALIAS** / **ANAME** for apex, you may use that pointing to `heng-kuang-venturo.github.io` instead of the A records — otherwise use the four A records above.

### www (`www.rootmarks.com`)

| Type | Name | Value |
|------|------|--------|
| CNAME | `www` | `heng-kuang-venturo.github.io` |

TTL: 300–3600 is fine. Propagation can take minutes to a few hours.

## What to do in GitHub (after DNS is set)

1. Repo → **Settings** → **Pages**
2. Source: **Deploy from a branch** → `main` → `/` (root) → Save
3. Custom domain: `rootmarks.com` → Save  
   - GitHub should write/update the repo root `CNAME` file (already committed as `rootmarks.com`)
4. Optionally add `www.rootmarks.com` as well if the UI offers it; DNS CNAME for `www` should still point at `heng-kuang-venturo.github.io`
5. Check **Enforce HTTPS** once the certificate provisions (may take a short while after DNS verifies)

## Checklist

- [ ] Apex A records (or ALIAS) set
- [ ] `www` CNAME → `heng-kuang-venturo.github.io`
- [ ] Pages enabled from `main` / root
- [ ] Custom domain `rootmarks.com` saved in Pages settings
- [ ] DNS check passes in Pages UI
- [ ] Enforce HTTPS enabled
- [ ] Visit https://rootmarks.com and https://www.rootmarks.com

## Verify locally / CLI

```bash
dig +short rootmarks.com A
dig +short www.rootmarks.com CNAME
curl -sI https://rootmarks.com | head -5
```

Expected A answers include the `185.199.10x.153` set; www should CNAME to `heng-kuang-venturo.github.io`.

## Notes

- Company/brand name stays **Rootmark**; the domain is **rootmarks.com** (with an “s”).
- Until DNS propagates, https://heng-kuang-venturo.github.io/rootmark/ may also serve the site.
