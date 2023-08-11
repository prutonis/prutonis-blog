---
title: "Adding Comments to My Blog"
date: 2023-08-10T15:52:10+03:00
tags: ['hugo', 'blog', 'site', 'generator', 'giscus', 'comments']
keywords: ['hugo', 'blog', 'site', 'generator', 'giscus', 'comments']
categories: ['Blog']
showtoc: false
tocopen: false
---

# Motivation
Being relatively new to the world of blogging, I quickly realized that my recently created website was missing a crucial element – reader feedback. It was evident that I needed to find a way to bridge this gap and encourage readers to voice their opinions and thoughts on my posts.

# The Search for a Good Commenting Solution
My website is on GitHub and uses [Hugo](https://gohugo.io/) static site generation. So, I needed a commenting solution that fits this setup. Even though Hugo supports Disqus for comments, my experience with it wasn't good due to its slow speed and ads. I found Giscus as an alternative. However, Giscus has its good sides, like using GitHub Discussion and being open-source, but it also has some possible drawbacks.
Giscus might not have all the customization and features of other comment systems because it relies on GitHub Discussions, which could lead to to a less satisfactory commenting experience. Also, since it needs a GitHub account for commenting, people who don't want to make a separate account just to comment might not engage as much, especially if they want to stay private or don't know much about GitHub.

# Steps to set up Giscus
1. Create a public respository on GitHub (GH) to hold your site comments, GH guide can be found [here](https://docs.github.com/en/get-started/quickstart/create-a-repo).
2. Enable Discussions for the created repository, [GH docs](https://docs.github.com/en/repositories/managing-your-repositorys-settings-and-features/enabling-features-for-your-repository/enabling-or-disabling-github-discussions-for-a-repository).
3. Install Giscus app from [GH Marketplace](https://github.com/marketplace), direct link to install is [here](https://github.com/apps/giscus).
4. Suggestion: restrict access for Giscus only to specific repository created for comments in step 1. [![giscus.jpg](https://i.postimg.cc/kMZSFKMC/giscus.jpg)](https://postimg.cc/qgsgptCD)
5. Configure Giscus directly from their site. As result I got this code script tag:
```js
<script src="https://giscus.app/client.js"
        data-repo="prutonis/prutonis-comments"
        data-repo-id="R_k9DOKFLCjg"
        data-category="General"
        data-category-id="DLC_kwDOCFLCjs4CYe3b"
        data-mapping="pathname"
        data-strict="1"
        data-reactions-enabled="1"
        data-emit-metadata="0"
        data-input-position="top"
        data-theme="{{ .Site.Params.giscusTheme }}"
        data-lang="en"
        data-loading="lazy"
        crossorigin="anonymous"
        async>
</script>
```
6. To avoid direct theme editing, Hugo enables you to customize any theme using [Partial templates](https://gohugo.io/templates/partials/). So I created a new file `layouts/partials/giscus.html` with this content:
```html
{{- if (eq (.Site.Params.disableComments | default false) false) -}}
    {{- if (eq (.Params.disableComments | default false) false) -}}
        <script src="https://giscus.app/client.js"
                data-repo="prutonis/prutonis-comments"
                data-repo-id="R_kgDOKFLCjg"
                data-category="General"
                data-category-id="DIC_kwDOKFLCjs4CYe3b"
                data-mapping="pathname"
                data-strict="1"
                data-reactions-enabled="1"
                data-emit-metadata="0"
                data-input-position="top"
                data-theme="{{ .Site.Params.giscusTheme }}"
                data-lang="en"
                data-loading="lazy"
                crossorigin="anonymous"
                async>
        </script>
    {{- end -}}
{{- end -}}
```

7. I'm using the [PaperMod](https://github.com/adityatelange/hugo-PaperMod) theme, so I duplicated `themes/PaperMod/layouts/partials/comments.html` to `layouts/partials/comments.html` and made edits to include the newly created partial from step 6.
```go
{{- /* Comments area start */ -}}

{{ partial "giscus" . }}

{{- /* Comments area end */ -}}

```
8. Hugo config.yml setup:
```yaml
params:
  ...
  comments: true
  giscusTheme: preferred_color_scheme
  disableComments: false
  ...
```

###### The result:
[![comments.png](https://i.postimg.cc/L6DWbh49/comments.png)](https://postimg.cc/VdS4Sfbp)

# Wrap-Up
Thanks to GitHub, I am able to both host my website and facilitate comments for it. This free feature provided by GitHub is truly invaluable. In the future, I intend to explore the possibility of implementing a self-hosted commenting system like [Commento](https://github.com/adtac/commento) or [StaticMan](https://staticman.net/), and I will be sharing my experience on the blog.

P.S. Special thanks to [Justin Bird](https://www.justinjbird.me/about/) for the insightful [blog post](https://www.justinjbird.me/2023/adding-comments-to-a-hugo-site-using-giscus/) on setting up Giscus.  

Feel free to share your thoughts and join the conversation by leaving a comment using the newly added comment section on my blog. Your input and feedback are highly appreciated!