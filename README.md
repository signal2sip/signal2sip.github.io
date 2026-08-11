# signal2sip.github.io

Source for [signal2sip.github.io](https://signal2sip.github.io/), the
project site for [signal2sip](https://github.com/signal2sip/signal2sip)
(a native daemon bridging Signal calling to SIP/PBX).

Built with [Hugo](https://gohugo.io/) and the
[Hextra](https://github.com/imfing/hextra) theme (vendored as a git
submodule). 9 languages; the docs section is currently English +
Ukrainian only.

## Running locally

```
git clone --recurse-submodules https://github.com/signal2sip/signal2sip.github.io.git
cd signal2sip.github.io
hugo server
```

Requires Hugo **extended**, version **0.146.0 or newer** (the Hextra
theme's own minimum, per `themes/hextra/theme.toml`) - CI builds with
0.164.0 (see `.github/workflows/deploy.yml`), which is a safe version to
match locally too. No Node.js/npm step - the
theme ships its Tailwind CSS pre-built, and this site doesn't add any
Tailwind classes of its own that would need a rebuild (see
`layouts/_partials/navbar-title.html`'s and
`layouts/shortcodes/hextra/feature-card.html`'s own comments for why:
this site's build doesn't generate `hugo_stats.json`, so any new
utility class added in a local override wouldn't reliably make it into
the theme's already-compiled stylesheet - those two files use plain CSS
instead for anything that needed a new class).

If you cloned without `--recurse-submodules`, run
`git submodule update --init` before building.

## Deployment

`.github/workflows/deploy.yml` builds the site with Hugo and publishes
it straight to GitHub Pages on every push to `main` - the built output
is never committed to git (see `.gitignore`).

## License

Site content and templates: [MIT](LICENSE). The vendored Hextra theme
(`themes/hextra`) carries its own MIT license.

signal2sip is not affiliated with, endorsed by, or sponsored by Signal
Messenger, LLC or the Signal Technology Foundation.
