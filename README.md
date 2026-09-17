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

## Publish a video

1. Put the media file at its final relative path under `videos/` or `showcase/`.
2. Commit and push this repository. GitHub is the archival source of truth.
3. Upload the same path to R2:

   ```bash
   npx wrangler r2 object put foamcut-media/videos/demos/your-video.mp4 \
     --file videos/demos/your-video.mp4 \
     --remote
   ```

4. Confirm `https://media.foamcut.io/videos/demos/your-video.mp4` responds before adding an app link.

See `docs/deployment/media-r2.md` in `foamCut` for the complete delivery, cache, and offline-installer process.
