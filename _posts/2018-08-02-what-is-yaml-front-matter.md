---
layout: post
title: What is YAML Front Matter?
categories: yaml yml front-matter
image: https://images.unsplash.com/photo-1520291453334-bf27a7e0e500?ixlib=rb-0.3.5&ixid=eyJhcHBfaWQiOjEyMDd9&s=12e67f6513a32f2ab2053f406aa84c60&auto=format&fit=crop&w=1350&q=80
---

Lately I started tinkering around with framework for static site generation sites, and I saw something new that I did not know. The so called **YAML Front Matter** (or just **Front Matter**).

At first the name confused me quite a lot, but after a while I realized how simple it is. Front Matter is nothing else that a space at the beginning of your templates, that is used to define variables, in YAML format. That is it. Let's see an example with Markdown and with HTML

```html
---
slug: about
comments_enabled: false
---

<!DOCTYPE html>
<html>
    <head>
        <meta charset="utf-8" />
    </head>
<body>
    <header>
        <h1>About page</h1>
    </header>

    <main>...</main>
</body>
</html>
```

```md
---
published: true
---

# My first post

Hello world

## Another section

lorem lorem lorem lorem lorem lorem
```

There is not much more to it. It basically couples tightly the variables of your page, to the document itself.

There are a couple restrictions that is necessary to know, thought:

1. The Front Matter needs to come the first thing in the document. There must not be **anything** in front. Not even white space.
2. The Front Matter must be wrapped in what is called the triple dash \`---\`. This is not just like a comment block, or a random way to separate the YAML from the rest of the document. It must always use this three hyphens at the beginning and end of the variable list.

I hope this helps someone. Cheers!
