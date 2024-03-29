---
title: 🔄 Continuous Deployment (CI/CD)
description: Building a CI/CD pipeline with Forestry and GitHub Actions.
date: 2021-03-29
publishDate: 2021-03-29
tags: [CI/CD, Hugo, GitHub, Forestry]
---

Deploying a new post to this blog is pretty easy. I just run these two commands:

```bash
hugo
firebase deploy only:hosting
```

However, this does require me to be on my computer to do a deployment. If I want to fix a spelling mistake, publish a draft, or update some content on another page I would have to be at home, on my computer. I wanted to see what it would take to write and deploy something from my phone.

Conceptually, there are two things that need to happen:

1. I need to be able to write a post, in markdown, on my phone, and save it to GitHub.
2. When there is a new commit to the repository, I need kick off a deployment.

With these two pieces in place, I should be able to writes posts and publish changes (easily) from my phone.

## Writing in Markdown

It turns out there are several Android apps for writing in markdown. However, it's still a bit of a pain to commit it to GitHub. Initially, I assumed I would just do some type of copy/paste job to GitHub's mobile website. I know it's not ideal, but how else do `git commit` on android? Well, as it turns out, there is a whole set of services related to git-based content editing. Content management systems (CMS) have been around for a long time. WordPress, is a very popular and well known one. It turns out there are some newer services that let you save your data directly to a GitHub repository.

## Forestry

So, this isn't how I was originally planning to accomplish my goal, but I've been pretty happy with what I've discovered so far. I tried out a service called [Forestry](https://forestry.io/ 'Forestry'). With it you can create a new "site" and link it to a git repository.

![](/uploads/forestry-step0.png 'Forestry Site List')

I linked mine to GitHub. They also have support for BitBucket, Gitlab, and Azure Devops.

![](/uploads/forestry-step1.png 'Repository Providers')

After linking a repository, you can pick your static site generator. I picked Hugo. They also have support for Jekyll, VuePress, and Gatsby, Eleventy, and others.

![](/uploads/forestry-step2.png 'Hugo Option')

Forestry then imported my site and I saw all (three) of my blog posts show up.

![](/uploads/forestry-step3.png 'Forestry Posts')

The editor is a pretty straightforward WYSIWYG editor. I started writing this blog post on Forestry to test it out and it has worked pretty well. I saved my draft and saw a new commit added to my GitHub repository with the comment:

    Update from Forestry.io

Perfect! That wraps up step 1. I was able to write a post on my phone and save it to my GitHub repository.

## GitHub Actions

Now that I can write posts and commit changes to my repository, it was time to enable continuous deployments. I used [GitHub Actions](https://github.com/features/actions 'GitHub Actions') is run a job on every commit to the `dev` branch. This workflow leveraged pre-existing actions, so it was super quick to get up and running. The entire workflow file is less than 30 lines long and I saved it to `.github/workflows/main.yml`

```yaml
name: CI/CD
on:
  push:
    branches: [dev]
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v2

      - name: Setup Hugo
        uses: peaceiris/actions-hugo@v2
        with:
          hugo-version: '0.81.0'
          extended: true

      - name: Build Site
        run: hugo

      - name: Deploy to Firebase
        uses: w9jds/firebase-action@master
        with:
          args: deploy --only hosting
        env:
          FIREBASE_TOKEN: ${{ secrets.FIREBASE_TOKEN }}
```

Once this file was committed and there was a commit to the `dev` branch, I went to the `Actions` tab to view the build.

![](/uploads/forestry-step4.png)

Boom! The site was built and deployed in 30 seconds flat.

I did a few more tests from Forestry and it worked like a charm.

## Conclusion

Forestry is a neat little service that enabled me to more easily write and edit my blog, directly from my android phone. Paired with GitHub Actions, this quickly enabled continuous deployments whenever there was a change to the content stored in repository. Maybe now I'll do some more writing 😉

## Additional Notes

### Workflow Triggers

I originally triggered the workflow via the on push event, but it seemed a little weird to run a whole deployment whenever I made a change to a draft. I then tried a `production` branching strategy, where I would do open a pull request to `production` whenever I wanted to do a deployment. This ended up being really annoying. It turned a short spelling update into a long, multi-step process. I've lately landed on a hybrid approach. My workflow now runs on a schedule (every night) and via the `workflow_dispatch` event, which allows for manual starts. My `main.yml` file triggers section looks like this now:

```yaml
on:
  workflow_dispatch:
  schedule:
    - cron: '0 0 * * *'
```

### Hugo Modules

Hugo has migrated from installing themes with `git submodule` to [Hugo Modules](https://gohugo.io/hugo-modules/ 'Hugo Modules'). I originally was using a`git submodule`, which required this setting in the workflow checkout step:

```yaml
with:
  submodules: true
```

I've since migrated to Hugo Modules and have found it a lot simpler. With Hugo Modules, this extra option was no longer required.
