# 🚀 Course Site Setup Guide

Welcome to your new Next.js course website! This repository has been successfully transitioned from a standard Jekyll GitHub Pages site to a modern, fully-featured Next.js application, mirroring the structure of Brian Holt's *Complete Intro to React v9*.

## 🛠️ What Was Done

To achieve this migration, the following steps were performed:

1. **Cleaned Up Old Architecture:**
   - Removed the old Jekyll-based files (`_config.yml`, `_posts/` directory, and the old `index.md`).
2. **Imported Source Code:**
   - Pulled in the `main` branch of the [Complete Intro to React v9](https://github.com/btholt/complete-intro-to-react-v9) Next.js source code.
3. **Configured for GitHub Pages:**
   - **`next.config.js`**: Added `basePath` and `assetPrefix` pointing to `/skills-github-pages`. This is critical for Next.js to properly resolve CSS, JavaScript, and image assets when hosted in a GitHub Pages subdirectory.
4. **Updated GitHub Actions:**
   - **`.github/workflows/next.yaml`**: Removed the `fqdn` parameter (which previously forced deployment to the author's custom domain). Now, the workflow cleanly builds and deploys to your standard GitHub Pages domain.
5. **Personalized the Site:**
   - **`course.json`**: Updated the author to `Khalid Mahmoud` and linked your GitHub profile.
   - **`package.json`**: Changed the project name and author details.

## 📝 How to Manage Your Site

Because this site is built with Next.js and uses Markdown/MDX, it is very easy to maintain.

### Editing Lessons
All of the course content lives in the `lessons/` directory. 
- You can add, remove, or modify the `.md` files in these folders to write your own curriculum.
- If you add new folders or files, make sure to update the `meta.json` file inside that specific folder to control the ordering and titles in the sidebar.

### Updating Site Information
If you want to change the title of the course, update your social media links, or change the course description, edit the **`course.json`** file located in the root directory.

### Changing Images
- Your profile picture is located at `public/images/author.jpg`. Replace this file with your own photo (keeping the same name) to update the author image on the homepage.
- The site favicon and social share images are also inside the `public/images/` folder.

## 🚀 How Deployment Works

This repository is set up with Continuous Deployment using **GitHub Actions**.

1. Whenever you commit and push changes to the `main` branch, the GitHub Action automatically starts.
2. It installs the necessary dependencies, builds the Next.js static files, and pushes the compiled website to a special branch called **`gh-pages`**.
3. GitHub Pages then serves the site directly from that `gh-pages` branch.

### To make sure it goes live:
Make sure your GitHub repository settings are configured to serve from the correct branch:
1. Go to your repository on GitHub.
2. Click on **Settings** > **Pages** (on the left sidebar).
3. Under **Build and deployment**, set the Source to **Deploy from a branch**.
4. Set the Branch to **`gh-pages`** and click **Save**.

---
*Your site will be live at: [https://Khalid-MahmouD.github.io/skills-github-pages/](https://Khalid-MahmouD.github.io/skills-github-pages/)*

---

## 🛠️ Do It Yourself (DIY) - How to Build This From Scratch

If you ever want to replicate this setup on a brand-new repository without using an AI assistant, follow these exact steps from your terminal and code editor:

### Step 1: Clone your empty repo and the source repo
First, clone the empty repository you created on GitHub. Then, download the source code of the course you want to mirror.

```bash
# Clone your own repository
git clone https://github.com/YOUR_USERNAME/YOUR_REPO_NAME.git my-course-site
cd my-course-site

# Clone Brian Holt's source code into a temporary folder
git clone https://github.com/btholt/complete-intro-to-react-v9.git temp-repo

# Delete the .git history from the downloaded source code
rm -rf temp-repo/.git

# Copy all the files from the temporary folder to your repo
cp -a temp-repo/. .

# Delete the temporary folder
rm -rf temp-repo
```

### Step 2: Essential Next.js Configuration (`next.config.js`)
Since your site will be hosted on GitHub Pages inside a subdirectory (e.g., `github.io/YOUR_REPO_NAME/`), Next.js needs to know this so it doesn't break CSS and Image links.

Open **`next.config.js`** and add the `basePath` and `assetPrefix` lines:

```javascript
/**
 * @type {import('next').NextConfig}
 */
const config = {
  output: "export",
  basePath: "/YOUR_REPO_NAME",        // <-- Add this
  assetPrefix: "/YOUR_REPO_NAME/",    // <-- Add this
};

export default config;
```

### Step 3: Fix GitHub Actions Workflow (`.github/workflows/next.yaml`)
The original source code attempts to deploy to a custom domain (`react-v9.holt.courses`) and assumes it has permission to push to your repository. You must fix both of these issues.

Open **`.github/workflows/next.yaml`**:

1. **Add Write Permissions** under the `push` block so GitHub Actions can legally push the built website code to the `gh-pages` branch.
2. **Remove the `fqdn`** line at the bottom so it stops trying to deploy to Brian's custom domain.

Your final file should look like this:

```yaml
name: Deploy NextJS Course Site to GitHub Pages

on:
  push:
    branches:
      - main

# MUST ADD THIS BLOCK
permissions:
  contents: write

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@master
      - name: npm install, build
        run: |
          npm install
          npm run build
      - name: Deploy site to gh-pages branch
        uses: crazy-max/ghaction-github-pages@v2
        with:
          target_branch: gh-pages
          build_dir: out
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
```

### Step 4: Personalize and Push
Update the author names in `course.json` and `package.json`, then commit your changes to GitHub:

```bash
git add .
git commit -m "Initial course setup from scratch"
git push origin main
```

### Step 5: Enable GitHub Pages
Once the GitHub Action finishes running (check the "Actions" tab on GitHub):
1. Go to your repo **Settings**.
2. Click **Pages**.
3. Under **Build and deployment**, select **Deploy from a branch**.
4. Set the branch to **`gh-pages`** and click Save!