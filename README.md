# forkforward.github.io

The ForkForward organization site, published at <https://forkforward.dev/>.

It introduces ForkForward and links to the projects. Each project's documentation lives in that project's
repository and is published under `https://forkforward.dev/<repository>/`, for example
[dotnet-mapper](https://forkforward.dev/dotnet-mapper/).

The site is built with [Zensical](https://zensical.org). The page is in [docs/index.md](docs/index.md), the
configuration in [zensical.toml](zensical.toml).

## Preview

```
pip install -r requirements.txt
zensical serve
```

Then open <http://localhost:8000/>.

## Publishing

[.github/workflows/docs.yml](.github/workflows/docs.yml) builds the site on every pull request and publishes it on
every push to `main`.

One-time setup in Settings > Pages:

- Build and deployment > Source: **GitHub Actions**.
- Custom domain: **forkforward.dev**, then **Enforce HTTPS** once GitHub has issued the certificate.

The custom domain is set here and nowhere else. This is the organization site, so GitHub serves every project
site of the organization under the same domain: `ForkForward/dotnet-mapper` is served at
`https://forkforward.dev/dotnet-mapper/`, and `forkforward.github.io/...` redirects there. Project repositories
leave their own Custom domain setting empty.

There is no `CNAME` file: GitHub ignores it for sites published by a GitHub Actions workflow and keeps the
domain in the repository settings.

### DNS for forkforward.dev

At the DNS provider of `forkforward.dev`:

| Name | Type | Value |
|---|---|---|
| `@` | `A` | `185.199.108.153`, `185.199.109.153`, `185.199.110.153`, `185.199.111.153` |
| `@` | `AAAA` | `2606:50c0:8000::153`, `2606:50c0:8001::153`, `2606:50c0:8002::153`, `2606:50c0:8003::153` |
| `www` | `CNAME` | `forkforward.github.io` |
| `_github-pages-challenge-ForkForward` | `TXT` | the code GitHub shows when you verify the domain (use the exact name it shows too) |

Verify the domain for the organization first (organization Settings > Pages > Add a domain). A verified domain
cannot be taken over by another GitHub account's Pages site.

`.dev` domains are HTTPS only in every browser, so the site does not open until GitHub has issued the
certificate, which can take up to an hour after the DNS records resolve.

## Adding a project

Add a row to the table in [docs/index.md](docs/index.md) and to the table in the organization profile
([ForkForward/.github](https://github.com/ForkForward/.github), `profile/README.md`).
