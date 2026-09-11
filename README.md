# foamcut-media

Published FoamCut tutorial videos, promo clips, and showcase files.

This repo is the git source of truth. Cloudflare R2 (custom domain
`media.foamcut.io`, plus a Cloudflare origin rule for `foamcut.io/videos/*`
and `foamcut.io/showcase/*`) is what the website and in-app Help Hub play.

Do not put these binaries back in the main `foamCut` repo.

## Layout

- `videos/demos/` — narrated walkthroughs (`*--voice-talia.mp4`)
- `videos/promos/`
- `videos/clips/`
- `videos/loops/`
- `showcase/` — spiral / Chubby Fish proof assets

## Update from foamCut

After publishing a new MP4 in `store/public/videos`:

```bash
cd /path/to/foamCut
npm run media:push-repo
npm run media:sync-r2    # after wrangler login, until GitHub Action secrets are set
```

See `docs/deployment/media-r2.md` in foamCut for the Cloudflare/R2 dashboard steps.
