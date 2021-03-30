---
title: "My Tiny Projects 🚀"
date: 2021-03-13
publishdate: 2021-03-13
tags: [Angular, Hugo, Projects]
---

## Tiny Projects

The other day I was reading [Hacker News][4] and was inspired by an article written by [Ben Stokes][5], the creator of [tinyprojects.dev][1].

> Probably like you, I'm that person who is constantly coming up with lots of little project ideas.
>
> ...
>
> The goal of this website is to try and explore as many of these ideas as I can.
>
> — [Ben Stokes][1]

I love the idea of doing "tiny" projects. I have a list of projects ideas and websites on my phone that I never seem to get around too. The goal of _this_ site is to help motivate me to explore and document some of _those_ ideas. The first idea in my list is to build a blog 😁.

## Angular

I come from a web development background that started with [AngularJS][6], which naturally has evolved into [Angular][7]. I do enjoy developing with a framework that _just comes_ with so many things ready to use out of the box. Angular includes:

- A CLI to generate components, services, pipes, modules, etc.
- Lazy loaded modules
- Routing
- Guards
- Dependency injection
- Translations
- Localization
- Less/sass support
- Typescript
- Linting
- And more...

In my opinion, the increased productivity gains are worth it for large application. They have to be in order to justify the mind-blowing bundle size that is angular... However, a simple blog like this is _not_ a large, complicated application that requires any of that stuff. Or, at least, it doesn't have to be. I have started to build a blog using angular before, but I just can't stomach deploying 500KB+ of javascript for a... blog.

Enter _static site generators_.

## Hugo

If you have ever researched building a blog, you have probably heard of [Hugo][2]. It is a _very fast_ static site generator. It is written in [Go][3], which is already known for being performant. The idea of a static site generator is to take in structured data (posts, pages, etc.), render them once (at build time), and output static html, which can be easily hosted (for free). Hugo seemed easy enough to install and use, so I decided to give it a try.

I chose to use the [PaperMod][8] theme, which was as simple as cloning a repo in the `themes` directory and adding some options to `config.yml`. Easy enough, right? Building this blog has been super simple (so far). I'd definitely recommend giving it a try. There is a vast collection of themes available for a variety of use cases, including blogs, portfolios, and personal sites. Check them out [here][9].

[1]: https://tinyprojects.dev/
[2]: https://gohugo.io
[3]: https://golang.org
[4]: https://news.ycombinator.com
[5]: https://twitter.com/tinyprojectsdev
[6]: https://angularjs.org
[7]: https://angular.io
[8]: https://adityatelange.github.io/hugo-PaperMod/
[9]: https://themes.gohugo.io/
