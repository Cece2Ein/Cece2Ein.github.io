---
title: "Carve out a corner with Hugo and Github"
date: 2023-06-28T17:30:01-07:00
draft: false
---
# Overview
Sometimes it takes a gym membership to embark on lifting weights, sometimes it takes signing up for a seminar to start reading the bookmarked arXiv papers, sometimes it takes a virtual publishing house to begin writing. 

Let's carve out a corner on the web for ourselves, friends, and serendipitous visiters. 

Hugo is an open-source static site generator. It's speedy and supports multi-languages. Github pages can host websites for individuals, organizations and projects. 

Guide below assumes a Mac. Sources for alternative machines and environments are linked when appropriate. 

# Tools

Install Git, Hugo, and sign up for a Github account.

**Git**, a tracking bug you actually like

    git --version 
Prints out the version of git or prompt to install.

**Hugo**, be romantic and creative like Victor

    brew install hugo

Install Hugo via package manager brew. Alternative installation methods are [here](https://gohugo.io/installation/macos/).

[Github](https://github.com/join), your web home

Be thoughtful when picking your user name, as it will be your web home name "https://<\your github username>.github.io/".

Alternative web homes see [here](https://gohugo.io/hosting-and-deployment/). 
# Steps
## 1. Set up the local home

In your terminal, choose a location to create a directory for your web home's local replica, then create a folder called mycorner with command `hugo new site`.  

    cd ~/Documents/projects/
    hugo new site mycorner

## 2. Choose a theme

Pick a theme [here](https://themes.gohugo.io/) and follow instructions on installation. An example with theme [Tokiwa](https://themes.gohugo.io/themes/hugo-theme-tokiwa/) is

    cd mycorner
    git init
    git submodule add https://github.com/heyeshuang/hugo-theme-tokiwa.git themes/hugo-theme-tokiwa 

## 3. Make your corner comfi
Edit the hugo.toml to personalize the theme to your taste and needs. The configuration used to generate the Tokiwa [demo site](https://heysh.xyz/hugo-theme-tokiwa/) is [here](https://github.com/heyeshuang/hugo-theme-tokiwa/blob/master/exampleSite/config.toml)

Minimal changes include

    author = "Your name"
    baseURL = "https://<your github username>.github.io/"
    copyright = "Copyright © <this year>"

## 4. Write your first post - about

    cd mycorner
    hugo new about.md
    cd mycorner/content
    vim about.md

Edit about.md using vim or other tools of choice. 

## 5. Test the site locally 

    cd mycorner
    hugo server
Open the generated link http://localhost:1313/ in your web browser to preview. 

## 6. Host on GitHub 

Generate the site

    cd mycorner
    hugo

### Create a git repo
Create a new public repo named *username*.github.io. You don't need to include a readme.

### Set up .gitignore
    vim .gitignore
Include the following

    # lock
    *.lock

    # hugo
    public/
    resources/

The public folder is generated fresh each time you `hugo`. And resources folder stores cashed files for faster site generation. Therefore you don't need to track them. See more explanations of the directory structure [here](https://gohugo.io/getting-started/directory-structure/)

Add more to the list as you go, such as executables, runtime data, or credentials. 
### Push to GitHub

    git add --all
    git commit -m "initial commit"
    git clone http://github.com/username/username.github.io
    git push -u origin main

### Host it on GitHub via Actions

Follow instructions [here](https://gohugo.io/hosting-and-deployment/hosting-on-github/)

## Future workflows
    hugo server -D
    hugo server --buildDrafts
    hugo -D
    hugo --buildDrafts
When creating content, the yaml by default includes tag `draft:true`.  Use flag `-D` or `--buildDrafts` to preview or generate the drafts in the public folder. When ready to publish the drafts, you can set the tag as `draft:false` or delete the tag. 

Alternatively, you can set the `date` to a future date for drafts. Use flag `--buildFuture` in testing and site generation.  

Another useful tag is `expiryDate`. Once set, stale posts are exluded from the build. Use flag `--buildExpired` to view them. 

Finally, flags can be stacked to view all past, current and future drafts or posts. 

Fancier, you can customize the defaults by using archetypes. 