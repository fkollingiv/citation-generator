# Shared Resource Citation Generator — Website Setup Instructions

These instructions cover:

1. Creating the GitHub repository and enabling GitHub Pages
2. Replacing the current inline code on `omics.dartmouth.edu/shared-resource-acknowledgment-generator/` with the iframe embed

---

## Step 1: Create the GitHub Repository

Repo name suggestion: **`citation-generator`** (matches the naming style of your existing `gsr-cost-calculator` repo).

### Option A — Using GitHub Desktop / the web UI

1. Go to https://github.com/new
2. Set **Repository name** to `citation-generator`
3. Set visibility to **Public** (required for free GitHub Pages)
4. Do **not** initialize with a README, .gitignore, or license — we'll push our own
5. Click **Create repository**
6. Open the new local folder (`citation-generator/`) in GitHub Desktop and publish it to the new repo

### Option B — Using the command line

Open a terminal in the `citation-generator/` folder (sibling to `gsr-cost-calculator/`) and run:

```bash
git init
git add .
git commit -m "Initial commit: shared resource citation generator"
git branch -M main
git remote add origin git@github.com:fkollingiv/citation-generator.git
git push -u origin main
```

(If you prefer HTTPS over SSH, swap the remote URL to `https://github.com/fkollingiv/citation-generator.git`.)

---

## Step 2: Enable GitHub Pages

1. In the new repo on github.com, go to **Settings → Pages**
2. Under **Build and deployment → Source**, select **Deploy from a branch**
3. Under **Branch**, choose `main` and `/ (root)`, then click **Save**
4. Wait ~30–60 seconds for the first deploy
5. The live URL will be: **https://fkollingiv.github.io/citation-generator/citation-generator.html**

Open that URL in a new tab and confirm the widget renders.

---

## Step 3: Replace the Inline Code on omics.dartmouth.edu

The current page at `omics.dartmouth.edu/shared-resource-acknowledgment-generator/` has the full HTML/CSS/JS pasted into a Custom HTML block. We'll swap that for an iframe so future updates require only a `git push`.

1. In your WordPress dashboard for `sites.dartmouth.edu/omics`, open the page **Shared Resource Citation Generator** for editing
2. Find the **Custom HTML** block that currently contains the widget code
3. **Delete the entire contents** of that block
4. **Paste the snippet below** into the same block:

```html
<iframe id="citationGenerator"
        src="https://fkollingiv.github.io/citation-generator/citation-generator.html"
        style="width:100%; border:0; min-height:900px;"
        title="Shared Resource Citation Generator"></iframe>
<script>
  (function () {
    var f = document.getElementById('citationGenerator');
    window.addEventListener('message', function (e) {
      if (!e.data || !e.data.type) return;
      if (e.data.type === 'citation-generator:height' && f) {
        f.style.height = e.data.height + 'px';
      }
    });
  })();
</script>
```

5. Click **Preview** and confirm the widget renders correctly (it should grow/shrink as categories are toggled or resources are selected — that's the postMessage auto-resize at work)
6. Click **Update** to publish

---

## Updating the Generator in the Future

Whenever a shared resource adds a new RRID, gets a new grant number, or changes its director:

1. Edit the `resources` array in `citation-generator.html`
2. `git commit && git push`
3. GitHub Pages republishes automatically (usually within 30 seconds)
4. Every page that embeds the iframe — including omics.dartmouth.edu — picks up the new version on next page load

No WordPress edit is ever needed again.

---

## Notes

- The widget is entirely self-contained — no external dependencies, no CDN calls, no analytics.
- Brand color: Dartmouth green (`#00693E`).
- The iframe wrapper script listens for `citation-generator:height` messages from the embedded page and resizes the iframe to fit its content, so users don't see internal scrollbars.
- If you ever rename the repo or move it to a Dartmouth org, update the `src` URL in the iframe snippet on the WordPress page accordingly.
