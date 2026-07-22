# travis-brand-studio

Browser-based motion-graphics studio for the Travis intro/outro
animation. Select any element, pick an effect, scrub the timeline, hit
record.

## Run locally

Any static server works:

```sh
npx serve .
# or
python -m http.server
```

## Deploy

Single `index.html`. Drop it anywhere:

```sh
# Cloudflare Pages
npx wrangler pages deploy . --project-name travis-brand-studio

# GitHub Pages: Settings → Pages → Deploy from a branch → main / (root)
```

## What it does

- **Presets** — pick a full recipe (Signature, Typewriter, Cascade,
  Snap, Broadcast, Minimal). Presets set every element's effect and
  timing at once.
- **Per-element effects** — click any element on the canvas (or in the
  layer list) to select it, then swap its effect. Text supports
  `fade-up`, `fade-in`, `slide-left/right`, `scale-in`, `typewriter`,
  `split-in`, and `stagger-up`. The orb has `rise-breath`, `glow-in`,
  and `pulse`.
- **Timeline scrubbing** — progress bar under the canvas is
  drag-to-seek. Space toggles play/pause. Arrow keys nudge ±0.1s.
- **Transport overlay** — play/pause button center-of-canvas,
  auto-hides during playback, returns on mouse move.
- **Layer visibility** — eye icon in each layer row toggles it off.
  The Minimal preset uses this to hide the orb.
- **Theme** — Dark or Light. Baked into the recorded video.
- **Orientation** — 16:9, 9:16, or 1:1. Native res up to 1920×1920.
- **Duration** — 4s / 5s / 8s / 12s. Longer holds work well as outros.

## Output

WebM at 10 Mbps. Chrome and Edge produce VP9; Safari falls back.
Convert to MP4 with:

```sh
ffmpeg -i travis-signature-dark-16x9-5s.webm -c:v libx264 -pix_fmt yuv420p out.mp4
```

Every serious video editor (Premiere, Final Cut, DaVinci Resolve,
CapCut) imports WebM directly.

## Fonts

Matches the usetravis.com stack: `Inter` for sans (with system
fallbacks) and `ui-monospace` for the wordmark. If you want the exact
Inter look everywhere, drop `Inter-Variable.woff2` at
`assets/fonts/Inter-Variable.woff2` and add a `@font-face` declaration
to the top of the `<style>` block.

## Keyboard

| Key | Action |
|---|---|
| Space | Play / pause |
| ← / → | Seek −0.1s / +0.1s |
| R | Record |
