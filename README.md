# Recline — GitHub Pages website

A static landing page and complete setup guide for Recline, the iPhone trackpad and keyboard for macOS. Ready for **GitHub Pages → Deploy from a branch → main → /(root)**.

No package installation, build step, custom GitHub Actions workflow or server is required for this website. All styling and branding assets are included. It works with both a project site (`https://YOUR-USERNAME.github.io/YOUR-REPOSITORY/`) and a user site (`https://YOUR-USERNAME.github.io/`) because asset and download URLs are relative.

## Repository layout

```text
index.html                         Website entry point, at repository root
.nojekyll                          Serve the static files without Jekyll
.gitignore                         Excludes local clutter and private configuration
README.md                          These instructions
assets/
  styles.css                       Responsive styling and print layout
  app-icon.svg                     Main logo
  status-logo.svg                   Header silhouette
  favicon.png                      Browser icon
downloads/
  Recline-macOS-arm64.zip           Ready-to-download Apple Silicon Mac app
  SHA256SUMS                       SHA-256 checksum for that archive
```

## Deploy using main / (root)

1. Create a GitHub repository (a public repository is the simplest option for GitHub Pages).
2. Extract this package. Copy its **contents** into your repository root: `index.html`, `assets/`, `downloads/`, `.nojekyll`, `.gitignore` and `README.md`. Do not put them inside an extra `recline-github-pages/` folder, and do not upload only the package ZIP.
3. Commit and push these files to **main**.
4. Open the repository's **Settings → Pages**.
5. Under **Build and deployment**, choose **Deploy from a branch**.
6. Select **main**, select **/(root)**, and click **Save**.
7. Wait for GitHub's deployment to finish. The Pages settings show the resulting site URL. Enable **Enforce HTTPS** when available.

Use Git when possible so the hidden `.nojekyll` file is included. The filename must be exactly `index.html` in the root of the selected branch.

For a new, empty GitHub repository, you can use the following commands from the folder containing `index.html`. Replace `YOUR-USERNAME` and `YOUR-REPOSITORY` with your real values:

```sh
git init -b main
git add .
git commit -m "Add Recline website"
git remote add origin https://github.com/YOUR-USERNAME/YOUR-REPOSITORY.git
git push -u origin main
```

For an existing repository, copy the files into its current checkout and commit/push normally; don't repeat `git init` or add a duplicate `origin` remote.

Official instructions: [Configure the Pages publishing source](https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site), [Create a Pages site](https://docs.github.com/en/pages/getting-started-with-github-pages/creating-a-github-pages-site).

## Preview locally

Open `index.html` in your browser, or run the following from the repository root:

```sh
python3 -m http.server 8000
```

Then open `http://localhost:8000`. Python is optional and used only for this local preview; GitHub Pages serves the files directly.

## Edit the site

- **Copy and setup instructions:** edit `index.html`.
- **Colours, typography and responsive layout:** edit `assets/styles.css`.
- **Branding:** replace the files in `assets/`, keeping their names or updating the corresponding HTML links.
- Keep local file URLs relative (`./assets/...`, `./downloads/...`). Leading-slash paths such as `/assets/...` can break a project site hosted below a repository name.

After editing, commit and push to `main`; GitHub Pages deploys that branch automatically once configured.

## Update the app download

1. Replace `downloads/Recline-macOS-arm64.zip` with the new app archive, keeping its filename. Avoid extracting the `.app` into the website repository.
2. Update the version text in `index.html` (currently `1.1.1`, in the hero and footer).
3. Refresh the checksum from the repository root:

```sh
(cd downloads && shasum -a 256 Recline-macOS-arm64.zip > SHA256SUMS)
```

4. Commit and push to `main`.

The included build is for Apple Silicon Macs and is not Developer ID signed or notarized. The page explains the required Mac permissions and iPhone certificate setup. Certificate **full trust** is a separate step after profile installation.

## Website versus remote-control service

GitHub Pages hosts the description, setup guide and app download. **The input server still runs inside Recline on each user's Mac.** Users scan their Mac's QR and connect Safari directly to that Mac; the GitHub Pages URL is not a replacement for the local trackpad URL.

The website does not include or install any individual's certificate, private key or pairing code. Certificates are generated on each user's Mac. Do not add the Mac's `Library/Application Support/Recline/HTTPS` folder to this repository.

This package does not configure a custom domain, publish a website or create a GitHub repository. You control when and where it is deployed. No license has been assigned on your behalf; add one if you want to grant reuse rights.
