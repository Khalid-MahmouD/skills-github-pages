---
description: Learn how to configure your new site and add new pages.
keywords:
  - setup
  - documentation
---

# Setup & Configuration

To make this site your own, you'll want to configure a few things. 

## 1. Edit `course.json`

The file `course.json` in the root of the repository controls the metadata of your site. 

You can change:
- Your `title` and `description`.
- The `author` details (your name and company).
- Your social media links (GitHub, LinkedIn, Twitter/X).

## 2. Customize Images

If you check the `public/images/` folder, you will see a few important images:
- **`author.jpg`**: Your profile picture displayed on the homepage.
- **`course-icon.png`**: The icon displayed in the main jumbotron header.
- **`social-share-cover.jpg`**: The image shown when your site is shared on social media.

Replace these with your own images (keeping the same file names) to personalize your site.

## 3. Sidebar Configuration (`meta.json`)

To order the links in the sidebar, you use a `meta.json` file inside each folder.

For example, this section's `meta.json` looks like this:

```json
{
  "title": "Getting Started",
  "icon": "play",
  "introduction": "Introduction",
  "setup": "Setup"
}
```

The key corresponds to the markdown filename (without the ordering prefix `A-` or the `.md` extension), and the value is the **Display Name** you want to show in the sidebar. The `icon` property dictates the FontAwesome icon used next to the section title!