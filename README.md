# Injustice Lab — flat mobile-upload package

This edition is prepared for GitHub's **Upload files** page on mobile. Upload all five files into your repository's **root** (not a `site/` directory), preserving their names.

Files: `index.html`, `app.js`, `styles.css`, `catalog.js`, `README.md`.

The app runs as a static website. It stores your builds locally in your browser. Back them up using its JSON export feature.

## Deploy using GitHub Actions (manual workflow)

1. Commit the five files above to `main`.
2. In the repository select **Add file → Create new file**.
3. Type `.github/workflows/deploy.yml` as the new file name (GitHub creates the folders automatically).
4. Paste the workflow from the ChatGPT instructions accompanying this ZIP, then commit it to `main`.
5. In **Settings → Pages**, select **GitHub Actions** under **Build and deployment**.
6. Open **Actions** to check the deployment result.

The deployment workflow needs to upload the repository root (`path: .`), not `site/`.

## Scope and limits

Prototype card/gear library and heuristic team grading, not a verified complete combat simulation. Manually-entered stats and research notes are separate from actual live game data.
