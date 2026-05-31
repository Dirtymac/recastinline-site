# Recast Inline — download site

Static landing page for distributing the **Recast Inline** test build. These files are meant
to live in a **separate public repo** (`Dirtymac/recastinline-site`) served via GitHub Pages.
The app's source code stays in the private `Dirtymac/RecastInline` repo.

## One-time setup

1. **Create the public site repo** and push these files (`index.html`, `style.css`) to its
   `main` branch:
   ```sh
   gh repo create Dirtymac/recastinline-site --public
   # copy index.html + style.css into it, commit, push to main
   ```

2. **Enable GitHub Pages:** repo Settings → Pages → *Deploy from a branch* → `main` / root.
   The site goes live at `https://dirtymac.github.io/recastinline-site/`.

3. **Create a release-publishing token** so the private repo's CI can push the DMG here:
   - GitHub → Settings → Developer settings → **Fine-grained tokens** → Generate new token.
   - Repository access: **only** `recastinline-site`. Permissions: **Contents → Read and write**.
   - In the **private** repo (`Dirtymac/RecastInline`): Settings → Secrets and variables →
     Actions → new secret named **`SITE_RELEASE_TOKEN`** with that token's value.

## Releasing a new build

From the **private** repo:
```sh
git tag v1.0 && git push origin v1.0
```
The `Release DMG` workflow builds the DMG and publishes it to this repo's Releases. The
download button (`releases/latest/download/RecastInline.dmg`) always points to the newest one,
so the HTML never needs editing per release.

## Notes
- The DMG is an ad-hoc-signed, un-notarized test build — the install steps on the page walk
  testers through the one-time Gatekeeper bypass.
- Don't commit the DMG into this repo; it's served as a Release asset.
