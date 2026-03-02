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