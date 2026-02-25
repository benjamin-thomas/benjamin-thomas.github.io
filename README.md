# benjamin-thomas.github.io

My personal blog, built with [Zola](https://www.getzola.org/) and the [zola-hacker](https://github.com/en9inerd/zola-hacker) theme.

## Prerequisites

Install Zola: https://www.getzola.org/documentation/getting-started/installation/

## Local development

```bash
# Clone with submodules
git clone --recurse-submodules git@github.com:benjamin-thomas/benjamin-thomas.github.io.git

# Or if already cloned
git submodule update --init --recursive

# Run the dev server
zola serve
```

The site will be available at `http://127.0.0.1:1111/`.

## Creating a new post

```bash
# Create a new file in content/posts/
cat > content/posts/my-new-post.md << 'EOF'
+++
title = "My New Post"
date = 2024-01-01
description = "A short description"

[taxonomies]
tags = ["Tag1", "Tag2"]
+++

Post content goes here...
EOF
```

## First-time deployment

### 1. Commit and push

```bash
git add -A
git commit -m "Migrate blog from Hugo to Zola"
git push origin master
```

### 2. Configure GitHub Pages to use Actions

The deploy action (`shalzz/zola-deploy-action`) builds the site and force-pushes the
result to a `gh-pages` branch. So GitHub Pages needs to serve from that branch:

1. Go to https://github.com/benjamin-thomas/benjamin-thomas.github.io/settings/pages
2. Under **Build and deployment > Source**, select **Deploy from a branch**
3. Under **Branch**, select `gh-pages` / `/ (root)`
4. Click **Save**

The first push to `master` will trigger the Action, which creates the `gh-pages` branch.
If the branch doesn't exist yet when you configure Pages, push first, wait for the Action
to finish, then configure.

### 3. Verify

After the Action completes, visit https://benjamin-thomas.github.io/ and confirm the site
is live.

## Enabling giscus comments

After the site is deployed:

### 1. Enable Discussions

Go to https://github.com/benjamin-thomas/benjamin-thomas.github.io/settings
Under **Features**, check **Discussions**.

### 2. Install the giscus app

Go to https://github.com/apps/giscus and install it for the
`benjamin-thomas/benjamin-thomas.github.io` repository.

### 3. Get your repo_id and category_id

1. Visit https://giscus.app/
2. Enter `benjamin-thomas/benjamin-thomas.github.io` as the repository
3. Select **Discussions** category: "Comments" (or whichever you prefer)
4. The page will generate a `<script>` tag — copy the `data-repo-id` and
   `data-category-id` values

### 4. Update zola.toml

Replace the `PLACEHOLDER` values in `[extra.giscus]`:

```toml
[extra.giscus]
repo_id = "paste-your-repo-id-here"
category_id = "paste-your-category-id-here"
```

### 5. Push the change

```bash
git add zola.toml
git commit -m "Configure giscus comment system"
git push origin master
```

## Ongoing deployment

Push to `master` and GitHub Actions will automatically build and deploy the site.
