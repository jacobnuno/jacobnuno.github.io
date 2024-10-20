---
layout: post
title:  "Create your first blog"
date:   2024-10-10
categories: blogging how-to jekyll web-development
tags: jekyll github-pages blog-setup static-site seo markdown
---

I always wanted a blog where I could get started quickly, make it SEO-friendly, and just focus on writing. Now, I’m going to show you how to create your own blog just like mine—the one you're reading right now.

Let’s get straight into it. This how-to guide will be as simple as installing a few things, doing some copy-pasting, and choosing a blog name (the hardest part, honestly).

_Pro tip: This tutorial shouldn’t take more than 15 minutes to set up, excluding installation time._

## Prerequisites:
- A GitHub account. The free version is fine, no need to pay to follow this tutorial.
- Ruby version 2.5.0 or higher (I’m using 3.2.0).
- RubyGems.

See [requirements](https://jekyllrb.com/docs/installation/#requirements) for guides and more details.

***

### Steps to create your blog

### 1. Install the [prerequisites](https://jekyllrb.com/docs/installation/)

Follow the link above and get everything set up on your machine.

### 2. Set up Jekyll on your local machine

First, you’ll need to install **Jekyll** locally:

- Install Ruby (if you don’t have it yet): [Install Ruby](https://www.ruby-lang.org/en/downloads/).
- Install the Jekyll and Bundler gems:
  ```bash
  gem install jekyll bundler
  ```

### 3. Create a new Jekyll blog
Navigate to the directory where you want to create your blog and run:
```bash
jekyll new my-awesome-blog
```
This sets up the basic structure for your Jekyll blog.

> Using GitHub Pages – How It Works
> 
> When hosting your site on GitHub Pages, the URL where your blog is published depends on how you name your repository on GitHub.
> 1. Custom User Page URL:
> If you name your repository exactly as `<your-github-username>.github.io`. Then your blog will be available at:
> ```
> https://your-github-username.github.io/
> ```
>
> 2. Repository-Based URL:
> If you create a normal repository (e.g., `your-github-username/your-repo`), your blog will be hosted at:
> ```
> https://your-github-username.github.io/your-repo/
> ```

Now, switch into your new directory:
```bash
cd my-awesome-blog
```

### 4. Initialize a Git repository (optional):
Why is this optional? Well, you’ll eventually need to initialize a git repo to push your blog to GitHub for deployment, but I recommend doing it now. Why? If you commit the basic Jekyll template first, it’ll be easier to track changes when you start customizing your blog. It's totally up to you though.
```bash
git init
git add .
git commit -m 'initial commit'
```

### 5. Configure Jekyll
Open the `_config.yml` file and modify it to suit your needs:
```yaml
title: My awesome blog
description: "A simple description for my awesome blog"
baseurl: "" # Leave empty if your deploying to GitHub Pages at the root of your repo
url: "https://your-github-username.github.io" # GitHub Pages URL

# Build settings
theme: minima
plugins:
  - jekyll-feed # To automatically generate an RSS feed
  - jekyll-seo-tag # For better SEO

# Permalink structure for posts (year/month/day)
permalink: /:year/:month/:day/:title/
```
Don’t forget to replace `your-github-username` with your actual GitHub username.

### 6. Modify the Gemfile for GitHub Pages
Since you're using only plugins supported by GitHub Pages, update your Gemfile like this:
  1. Open the `Gemfile` in your project directory.
  2. Remove the Jekyll Gem
Since GitHub Pages manages the Jekyll version, comment out or remove the Jekyll gem from the `Gemfile`:
```bash
# gem "jekyll", "~> 4.3.4"
```
  3. Uncomment the GitHub Pages Gem
Uncomment the following line to include the GitHub Pages gem, which ensures compatibility with GitHub’s infrastructure:
```ruby
gem "github-pages", group: :jekyll_plugins
```
  4. Check for Extra Plugins Compatibility (optional)
Some plugins are already included with GitHub Pages. Here's what your plugins section should look like to avoid conflicts:
```ruby
group :jekyll_plugins do
  gem "jekyll-feed", "~> 0.12"
  gem "jekyll-seo-tag"
end
```
  5. Run `bundle install`
After making these changes, run the following command to update your dependencies:
```bash
bundle install
```
  6. Commit your changes
Don’t forget to commit the changes to your repository:
```bash
git add Gemfile Gemfile.lock
git commit -m "configure Gemfile for GitHub Pages"
```

### 7. Add your first blog post

Blog posts in Jekyll go in the `_posts` folder and follow this naming convention: `YYYY-MM-DD-title.markdown`.

For example, create a post like this: `2024-10-10-welcome-to-my-awesome-blog.markdown`.
```markdown
---
layout: post
title: "Welcome to my awesome blog"
date: 2024-10-10
categories: general
---

Welcome to my blog! This is my first post.
```

### 8. Push to GitHub and deploy with GitHub Pages
  1. If you haven’t initialized a Git repo yet, do it now (see step 4).
  ```bash
git init
git add .
git commit -m 'initial commit'
  ```
  2. Create a GitHub repository with the name `your-github-username.github.io`.
  3. Push your Jekyll blog to GitHub:
  ```bash
git remote add origin https://github.com/yourusername/your-github-username.github.io.git
git branch -M main
git push -u origin main
  ```

### 9. Review your project folder
After making these changes, your project folder should look like this:
```yaml
<your-github-username>.github.io/
├── _posts/                      # All your markdown blog posts go here
│   ├── 2024-10-10-welcome-to-jekyll.markdown
│   └── 2024-10-10-welcome-to-my-awesome-blog.markdown
├── _config.yml                  # Jekyll configuration file (site settings, plugins, etc.)
├── .gitignore                   # Git ignore file
├── 404.html                     # Custom 404 error page
├── about.markdown               # "About Me" page (markdown format)
├── Gemfile                      # Ruby dependencies (Jekyll and other gems)
├── Gemfile.lock                 # Locked versions of Ruby dependencies
└── index.markdown               # Home/
```


***

### Extra tips
Here are a few bonus tips to help you out:

#### 1. Overrides and customization
Jekyll themes, like the default Minima theme, are gem-based, which means some theme files are hidden in the gem and not directly accessible in your project. However, you can override any theme defaults by copying or creating files with the same name in your own project’s folders, such as `_layouts`, `_includes`, `_sass`, or `assets`.

For example, if you want to change the theme's layout, you can create a custom layout in the `_layouts` folder. Jekyll will prioritize your custom layout over the default one in the gem.
[Learn more about overriding theme defaults](https://jekyllrb.com/docs/themes/#overriding-theme-defaults)

#### 2. Understanding Gem-Based Themes
Jekyll uses gem-based themes to simplify updates and keep your project clean. With these themes, the assets, layouts, and includes are bundled within the gem, and only a few files like `_config.yml` and your posts are visible in your project. This approach keeps things streamlined but allows you to still customize everything by overriding specific files. 
[Check out how gem-based themes work here](https://jekyllrb.com/docs/themes/#understanding-gem-based-themes)

#### 3. Different templates
If you're not satisfied with the default Jekyll theme and want to explore other designs, you can find both free and paid themes at [Jekyll Themes](https://jekyllthemes.io/). However, note that **not all themes are supported by GitHub Pages**. GitHub Pages supports a specific set of themes like Minima, Architect, Cayman, and others. You can find the full list of supported themes [here](https://pages.github.com/themes/). Be sure to choose a theme that is supported if you're hosting your blog on GitHub Pages.

#### 4. Local server
Build your site and run it locally for testing:
```bash
bundle exec jekyll serve
```

#### 5. Live reload
Want live reloading when you make changes? Serve it like this:
```bash
bundle exec jekyll serve --livereload
```

#### 6. Debugging mode
If you run into issues, start Jekyll in verbose (debug) mode:
```bash
bundle exec jekyll serve --verbose
```

#### 7. Localhost
Browse your blog locally at: http://localhost:4000
