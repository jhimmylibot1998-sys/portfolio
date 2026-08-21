# Deploy Jimmy Libot’s Portfolio on GitHub Pages

This package is prepared for **free GitHub Pages deployment**. It includes every portfolio image, video, poster frame, and resume PDF inside `client/public/media/`, so it does not depend on Manus storage after deployment.

## 1. Create the GitHub repository

Sign in to [GitHub](https://github.com) and create a new repository named `jimmy-libot-portfolio`. A public repository works with GitHub Free and GitHub Pages. You can make the repository private while preparing it, but remember that a deployed GitHub Pages website is publicly accessible; remove any secrets or private client data before publishing.[1]

## 2. Upload this prepared package

Extract the ZIP file. Upload the **contents** of the `jimmy-libot-portfolio-github-pages` folder to the root of the new GitHub repository. Ensure that these files and folders are visible at the repository root:

```text
.github/workflows/deploy.yml
client/
server/
shared/
package.json
pnpm-lock.yaml
vite.config.ts
```

Commit the upload to the `main` branch. The included workflow will build the Vite site and deploy it whenever you push an update to `main`.

## 3. Enable GitHub Pages

Open the repository, then go to **Settings → Pages**. Under **Build and deployment**, choose **GitHub Actions** as the source. GitHub Pages needs this option because Vite must build the site before GitHub can publish it.[1] [2]

After the next push, open the **Actions** tab and wait for **Deploy portfolio to GitHub Pages** to finish with a green check mark. GitHub will show the deployed URL in the workflow summary and under **Settings → Pages**.

If your GitHub username is `YOUR-USERNAME` and your repository name is `jimmy-libot-portfolio`, the URL will be:

```text
https://YOUR-USERNAME.github.io/jimmy-libot-portfolio/
```

## Why this package works on GitHub Pages

Vite projects published from a repository path need the correct base path. The included deployment workflow dynamically builds with `/${repository-name}/`, so your images, videos, favicon, resume download, and CSS links resolve correctly at `https://YOUR-USERNAME.github.io/jimmy-libot-portfolio/`.[2]

The workflow uses Node 22 and pnpm 10, installs the locked dependencies, builds the Vite output, uploads `dist/public`, and deploys that static output to Pages. Do not change `path: ./dist/public` unless you also change the Vite output directory.

## Before sharing the link with clients

Replace the placeholder LinkedIn and YouTube URLs in `client/src/pages/Home.tsx`. The contact form currently displays a thank-you state but does not send email; connect it to an approved form service or backend before relying on it for enquiries. Also confirm you have permission to publish the barbecue client-work video and any client-specific visual material.

## Updating the website later

Make your changes, commit them, and push to `main`. The workflow redeploys the static site automatically. If a deployment fails, open **Actions → Deploy portfolio to GitHub Pages** and inspect the failed step. The common causes are uploading the outer folder instead of its contents, selecting a branch other than `main`, or not choosing **GitHub Actions** in Settings → Pages.

## References

[1]: https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site "Configuring a publishing source for your GitHub Pages site — GitHub Docs"

[2]: https://vite.dev/guide/static-deploy "Deploying a Static Site — Vite"
