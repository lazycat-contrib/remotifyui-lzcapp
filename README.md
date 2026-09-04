# RemotifyUI for LazyCat

LazyCat LPK v2 packaging for [RemotifyUI](https://github.com/ca-x/remotifyui), a self-hosted Remotify control plane with multi-user OIDC, scoped Agent APIs, and an embedded React UI.

The package persists SQLite and transfer data under `/lzcapp/var`, configures LazyCat OIDC at `/api/auth/oidc/callback`, and exposes all supported deployment settings through the setup wizard. The upstream Docker command does not define a healthcheck, so this package intentionally does not invent one.

## Build

```sh
lzc-cli project release -o dist/application.lpk
```

## GitHub Actions secrets

- `LZC_API_TOKEN`: LazyCat PAT used for image delivery and official publishing
- `LZC_API_HOST`: optional PAT API host override
- `APPSTORE_URL`: private store URL
- `APPSTORE_TOKEN`: private store token
- `APP_ID`: optional existing private-store application ID
- `PRIVATE_STORE_GROUP_CODES`: optional private-store group codes

The scheduled workflow discovers stable SemVer image tags, copies the selected `linux/amd64` image to the LazyCat registry, creates a versioned GitHub Release asset, and reconciles the official and private stores independently.
