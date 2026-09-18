# Image Prep for Flipkart

A free, single-page browser tool that batch-resizes and pads product photos to Flipkart's main-image spec:

- **2000×2000 px**
- **Pure white (#FFFFFF) background**
- **JPEG**, quality 85
- Product filling **~85%** of the frame

Everything runs client-side in the browser (HTML/CSS/JS + [JSZip](https://stuk.github.io/jszip/) from a free CDN) — no server, no build step, no paid API, no account needed to run it. Photos never leave the visitor's device.

> **Note:** this pads/resizes onto a white canvas — it does not cut out a busy background. For a clean white background, shoot your products on a plain white or light backdrop first. (True AI background removal needs a hosted model/API, which is outside the "free, no server" scope of this tool — see *Extending it* below if you want to add that yourself.)

## Run it locally

No install needed — just open `index.html` in any modern browser, or serve the folder:

```bash
npx serve .
# or
python3 -m http.server 8000
```

## Deploy for free with GitHub Pages

1. Create a new repository on GitHub (e.g. `image-prep-flipkart`) and push this folder to it:

   ```bash
   git init
   git add .
   git commit -m "Initial commit: Flipkart image prep tool"
   git branch -M main
   git remote add origin https://github.com/<your-username>/<your-repo>.git
   git push -u origin main
   ```

2. On GitHub, go to **Settings → Pages**.
3. Under **Build and deployment → Source**, choose **Deploy from a branch**.
4. Pick branch **main**, folder **/ (root)**, then **Save**.
5. GitHub will publish it at:

   ```
   https://<your-username>.github.io/<your-repo>/
   ```

   (takes 1–2 minutes to go live after the first push). No cost, no custom domain required — though you can attach a free subdomain (e.g. from [is-a.dev](https://www.is-a.dev/) or [eu.org](https://nic.eu.org/)) or your own domain later via the Pages **Custom domain** field if you want.

## Other free hosting alternatives

Since it's a static file with no server/build step, any of these work as drop-in alternatives to GitHub Pages, all on free tiers:

- **Cloudflare Pages** — drag-and-drop deploy from the dashboard, or connect the GitHub repo for auto-deploys.
- **Netlify** — same, with a free `*.netlify.app` subdomain.
- **Vercel** — same, with a free `*.vercel.app` subdomain.

## Project structure

```
.
├── index.html   # the entire app (markup, styles, logic)
└── README.md
```

## Extending it

- **True background removal**: swap the padding step for a client-side ML model such as [@imgly/background-removal](https://github.com/imgly/background-removal-js) (runs in-browser via WebAssembly, MIT-licensed, free) — note its model files (~40 MB) are fetched from a CDN at runtime, so this only works on hosts that allow that external fetch (GitHub Pages does; it will *not* work inside the Claude Artifact-hosted version of this tool, which sandboxes external requests).
- **Custom canvas size / coverage / quality**: edit the `TARGET`, `COVERAGE`, and `QUALITY` constants near the top of the `<script>` block in `index.html`.

## License

MIT — see `LICENSE`.
