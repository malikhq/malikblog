# Malik Personal Website

This repository contains the source code and configuration for my personal website **[MalikSite](https://malikhq.netlify.app/)**. The website is built using **Hugo**, a fast and flexible static site generator, and is deployed on **Netlify**.

The site showcases my portfolio, blog posts, projects, and other professional details.

---

## Table of Contents

* [Features](#features)
* [Prerequisites](#prerequisites)
* [Installing Hugo and Adding Theme](#installing-hugo-and-adding-theme)
* [Getting Started](#getting-started)
* [Commands](#commands)
* [Deployment](#deployment)
* [Project Structure](#project-structure)
* [Contributing](#contributing)
* [License](#license)

---

## Features

* Fast and lightweight static site built with Hugo.
* Clean, responsive design using the **nort** theme.
* Support for categories and tags for blog posts.
* SEO-friendly URLs and meta information.
* Integrated with **Netlify** for CI/CD deployment.

---

## Prerequisites

Before running this project locally, make sure you have:

* [Hugo](https://gohugo.io/getting-started/installing/) (version 0.149+ recommended)
* [Git](https://git-scm.com/)
* [Node.js & npm](https://nodejs.org/) (optional, for theme assets)
* [Netlify account](https://www.netlify.com/) (for deployment)

---

## Installing Hugo and Adding Theme

### Step 1: Install Hugo

Follow the official guide to install Hugo: [Hugo Installation](https://gohugo.io/getting-started/installing/).

Verify the installation:

```bash
hugo version
```

### Step 2: Add the Nort Theme

Clone the Hugo site and add the **nort** theme as a submodule:

```bash
git clone https://github.com/malikhq/malikblog.git
cd malikblog
git submodule add https://github.com/example/nort.git themes/nort
git submodule update --init --recursive
```

This will download the **nort** theme into the `themes/nort` directory.

---

## Getting Started

### Step 3: Serve the Site Locally

Run Hugo server to preview the site with drafts and future posts:

```bash
hugo server --buildDrafts --buildFuture
```

Open your browser at [http://localhost:1313](http://localhost:1313).

---

## Commands

### Build the Static Site

Generate the `public` folder for deployment:

```bash
hugo --minify
```

### Clean Cache (Optional)

```bash
hugo --cleanDestinationDir
```

---

## Deployment to Netlify

1. Create a site on Netlify.
2. Connect your GitHub repository.
3. Set the build command:

```bash
hugo --minify
```

4. Set the publish directory to:

```
public
```

Alternatively, use GitHub Actions for automated deployment:

```yaml
name: "Hugo Deploy to Netlify"

# Trigger workflow on push to main
on:
  push:
    branches:
      - main

jobs:
  build-and-deploy:
    name: "Build Hugo and Deploy"
    runs-on: ubuntu-latest

    steps:
      # 1. Checkout code
      - name: Checkout repository
        uses: actions/checkout@v4
        with:
          submodules: recursive

      # 2. Set up Hugo
      - name: Setup Hugo
        uses: peaceiris/actions-hugo@v3
        with:
          hugo-version: '0.149.0'  # Match the version you use on Netlify
          extended: true

      # 3. Build Hugo site
      - name: Build Hugo
        run: hugo --minify

      # 4. Install Netlify CLI
      - name: Install Netlify CLI
        run: npm install -g netlify-cli

      # 5. Deploy to Netlify
      - name: Deploy to Netlify
        uses: jsmrcaga/action-netlify-deploy@v2.0.0
        with:
          NETLIFY_AUTH_TOKEN: ${{ secrets.NETLIFY_AUTH_TOKEN }}
          NETLIFY_SITE_ID: ${{ secrets.NETLIFY_SITE_ID }}
          NETLIFY_DEPLOY_MESSAGE: "Deploy from main branch ${{ github.sha }}"
          NETLIFY_DEPLOY_TO_PROD: true
          build_directory: "public"
          install_command: "echo Skipping install"
          build_command: "echo Skipping build"
```

---

## Project Structure

```
malikblog/
├── archetypes/         # Hugo content templates
├── content/            # Markdown content for pages and posts
├── data/               # Data files (YAML, JSON)
├── layouts/            # Custom layouts and templates
├── static/             # Static assets (images, CSS, JS)
├── themes/             # Hugo theme(s)
├── config.toml         # Hugo configuration
├── public/             # Generated static site (after build)
├── package.json        # Optional, for assets
└── README.md
```

---

## Contributing

Contributions are welcome! You can:

1. Fork the repository.
2. Make changes in your branch.
3. Submit a pull request describing your updates.

---

## License

This project is licensed under the MIT License. See [LICENSE](LICENSE) for details.
