+++
date = 2021-03-26T07:00:00Z
draft = true
publishdate = 2021-03-26T07:00:00Z
tags = ["CI/CD", "Forestry"]
title = "Continuous Deployment"

+++
Deploying a new post to this blog is pretty easy. I just run these two commands:

```bash
hugo
firebase deploy only:hosting
```

However, this does require me to be on my computer to do a deployment. If I want to fix a spelling mistake, publish a draft, or update some content on another page I would have to be at home, on my computer. I wanted to see how hard it would be to write and deploy a post directly from my phone.

I decided to break it down into two parts.

1. Writing a new post on my phone and saving it to github. 
2. Configuring github to automatically build and deploy whenever there are changes pushed to the main branch.

## Writing in Markdown

It turns out there are several Android apps for writing in markdown. However, it's still a bit of a pain to commit it to Github. So, the writing seems doable, but the uploading piece is still questionable. After all, if it's too inconvenient I'd just end using my computer anyways. 

## Headless CMS

After a little bit of research, it turns out there are a few content management systems (CMS) that can edit content stored in git on github. There's actually a site called Forestry that understands Hugo sites and provides 