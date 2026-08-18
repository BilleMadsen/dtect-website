# DTECT — static site

A single static page. No build step, no dependencies, no server.
`index.html` contains the markup, styles and script inline.

```
index.html      the whole page
assets/         hero-broadcast.jpg, range-doppler.jpg, og.jpg (share preview)
favicon.svg
robots.txt
.nojekyll       stops GitHub Pages running the files through Jekyll
```

## Before you publish

Open `index.html` and replace `https://dtectsystems.eu/` in the three tags
marked `EDIT ME` with your real origin. `og:image` **must** be an absolute URL —
LinkedIn, X and Slack will not resolve a relative path, and the link preview
will come up blank.

If you publish to `https://<user>.github.io/<repo>/`, the origin includes the
repo name.

## Publishing to GitHub Pages

```bash
git init
git add .
git commit -m "DTECT site"
git branch -M main
git remote add origin git@github.com:<user>/<repo>.git
git push -u origin main
```

Then in the repo: **Settings → Pages → Source: Deploy from a branch**, branch
`main`, folder `/ (root)`. First deploy takes a minute or two.

### Custom domain

Add a file called `CNAME` containing just the hostname (`dtectsystems.eu`),
commit it, and set the same domain under Settings → Pages. Point a DNS `CNAME`
record at `<user>.github.io`, or `A` records at GitHub's four Pages IPs if you
are using the apex domain.

## Working on it locally

Any static file server will do:

```bash
python3 -m http.server 8000
```

Then open http://localhost:8000.

## How the enquiry form works

There is no backend. On submit the page builds a `mailto:` link and navigates
to it, which hands the pre-filled message to the visitor's mail client.

Because navigating to a `mailto:` never reports success or failure, the dialog
always follows up with a panel containing the full message and a copy button —
so a visitor with no mail client configured still has a way to reach you rather
than submitting into nothing.

Messages that would produce a `mailto:` URL over 1900 characters skip the
navigation entirely and go straight to the copy panel; long URLs get silently
truncated by Outlook and the Windows shell.
