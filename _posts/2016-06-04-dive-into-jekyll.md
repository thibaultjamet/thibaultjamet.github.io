---
title: Playing a bit more with jekyll
date: 2016-06-04 00:00:00 Z
layout: post
---

As expected, the first deployment went very smoothly. A simple push to the sources
repository has been enough to update [thibaultjamet.github.io](https://thibaultjamet.github.io).
It still does not look very nice and would need to have some kind of a sitemap and links
to my very first post.

## Content editing

Writing my first post made me go some issue where my markdown files
where not processed correctly by jekyll. After some quick googling it
appears that I didn't get/read the point where anything supposed to be
handled by jekyll must have a yaml block (frontmatter) at its top, as
explained in [this page](https://jekyllrb.com/docs/frontmatter/)

```yaml
---
---
```

## Tackling default folders

So far I played with:

- _layouts
    a folder in which you insert templatized html
- _drafts
    This is where you write articles for the future
    articles in this folder won't be generated by default
- _posts
    This is where the published posts are. They must contain
    the post date in their name YYYY-MM-DD

As I am a bit lazy, I don't want to bother writing the date by
hand for every new post, jekyll, clever they are, wrote a gem
jekyll-compose that allows to create publish and unpublish
posts, drafts and pages. The generated file will then contain
the frontmatter header as well as the date in case of a publised
post.

Moreover, the cli allows publishing a draft from its path,
inserting automatically the date. Pretty nice when you are a
bit lazy like me.

```sh
jekyll draft 'My page title'
jekyll publish _drafts/my-page-title.md
```

Awesome, it includes date generation and special caracters
escape.

## Layouts

But, jekyll-compose adds, by default, a layout to each page.
Then I added a file `_layouts/post.html` that contains 

```
---
layout: default
---
<article class="post-content">
{% raw %}{{ content }}{% endraw %}
</article>
```


<mark>Note</mark>: explaining this, I found out that we can insert templatized
values inside the post. Thus inserting {% raw %}{{ content }}{% endraw %}
may dump some page content:

---

{{ content }}

---
