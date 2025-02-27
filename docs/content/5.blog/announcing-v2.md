---
layout: article
navigation: false
title: 'Announcing Nuxt Content v2'
description: '2 years after the release of Content v1, we are proud to announce the second version of Nuxt Content built for Nuxt 3.'
cover: /announcing-v2.png
date: 2022-05-19
authors:
  - name: Sebastien Chopin
    avatarUrl: https://pbs.twimg.com/profile_images/1042510623962275840/1Iw_Mvud_400x400.jpg
    link: https://twitter.com/Atinux
  - name: Yael Guilloux
    avatarUrl: https://pbs.twimg.com/profile_images/1227208659572269056/Yo6GUjZw_400x400.jpg
    link: https://twitter.com/yaeeelglx
  - name: Farnabaz 
    avatarUrl: https://pbs.twimg.com/profile_images/780374165136244736/x5HfdWA1_400x400.jpg
    link: https://twitter.com/a_birang
  - name: Clement Ollivier 
    avatarUrl: https://pbs.twimg.com/profile_images/1370286658432724996/ZMSDzzIi_400x400.jpg
    link: https://twitter.com/clemcodes
tags:
  - Nuxt
  - Content
  - Release
category: Announcements
---

2 years after the [release of Content v1](https://github.com/nuxt/content/releases/tag/v1.0.0), we are proud to announce the second version of Nuxt Content built for [Nuxt 3](https://v3.nuxtjs.org).

On top of the Nuxt 3 support, we couldn't help adding new features:

::list{icon="heroicons-outline:badge-check"}
- The [MDC Syntax](/guide/writing/mdc) for Components in Markdown
- Internationalization support
- [Navigation generation](/guide/displaying/navigation)
- [Fully typed](/guide/displaying/typescript)
- [Multiple sources](/api/configuration#sources) (experimental)
- Live preview edition (coming soon)
::

## What is Nuxt Content?

Nuxt Content is a [Nuxt module](https://v3.nuxtjs.org/guide/features/modules) that reads Markdown, YAML, CSV and JSON files in the `content/` directory.

Let’s imagine a `content/` directory with the following structure:

::code-group
  ```[Directory Structure]
  content/
    hello.md
  ```
  ```md [hello.md]
  # Hello World

  My first paragraph.

  <https://content.nuxtjs.org>
  ```
::

Create a `pages/[...slug].vue` file with the [`<ContentDoc>`](/guide/displaying/rendering) component inside:

```vue [pages/[...slug].vue]
<template>
  <ContentDoc />
</template>
```

And voilà!

::code-group
  ::code-block{label="https://wonderful-app.com/hello" preview}
    # Hello World

    My first paragraph.

    https://content.nuxtjs.org
  ::
::

You can also query the `hello.md` file by using the `queryContent()` composable:

```ts
const file = await queryContent('hello').findOne()
```

::alert
  ::details
    :summary[The returned file won't be Markdown or HTML, but a JSON representing the abtract syntax tree.]
    ```json [document value]
    {
      "type": "markdown",
      "id": "content:hello.md",
      "source": "content",
      "path": "hello",
      "extension": "md",
      "atime": "2022-05-10T14:38:23.462Z",
      "mtime": "2022-05-10T14:38:23.462Z",
      "size": 63,
      "slug": "/hello",
      "draft": false,
      "partial": false,
      "empty": false,
      "title": "Hello World",
      "description": "My first paragraph.",
      "body": {
        "type": "root",
        "children": [
          {
            "type": "element",
            "tag": "h1",
            "props": {
              "id": "hello-world"
            },
            "children": [
              {
                "type": "text",
                "value": "Hello World"
              }
            ]
          },
          {
            "type": "element",
            "tag": "p",
            "props": {},
            "children": [
              {
                "type": "text",
                "value": "My first paragraph."
              }
            ]
          },
          {
            "type": "element",
            "tag": "p",
            "props": {},
            "children": [
              {
                "type": "element",
                "tag": "a",
                "props": {
                  "href": "https://content.nuxtjs.org",
                  "rel": [
                    "nofollow",
                    "noopener",
                    "noreferrer"
                  ],
                  "target": "_blank"
                },
                "children": [
                  {
                    "type": "text",
                    "value": "https://content.nuxtjs.org"
                  }
                ]
              }
            ]
          }
        ],
        "toc": {
          "title": "",
          "searchDepth": 2,
          "depth": 2,
          "links": []
        }
      }
    }
    ```
  ::
::

You can do much more than fetch only one file, take a look at the [querying content](/guide/displaying/querying) section to discover its full potential.

## Introducing MDC

We wanted to leverage the power of Vue components in a content edition experience. After months of testing on the [Nuxt website](https://nuxtjs.org), we are happy to introduce the [**M**ark**D**own **C**omponents syntax](/guide/writing/mdc).

::list{icon="heroicons-outline:badge-check"}

- Use your own Vue components in Markdown
- Customize them with props
- Write Markdown content in slots (and of course, you can nest them)
- Experience blazing fast HMR for Markdown and MDC (as fast as Vite!)
::

::alert
MDC is Markdown, so nothing changes and you can keep using the `.md` extension.
::

### Show me how it works!

::code-group

  ```md [content/index.md]
  ::my-button{type="success"}
    ✏️ Start **writing!**
  ::
  ```

  ::code-block{label="Preview" preview}
    <MyButton type="success">✏️ Start <strong>writing!</strong></MyButton>
  ::

  ```vue [components/MyButton.vue]
    <script setup>
      defineProps({
        type: {
          type: String,
          default: 'info'
        }
      })
      </script>

      <template>
        <button :class="type">
          <Markdown unwrap="p" />
        </button>
      </template>
  ```

::

Head over to the [MDC guide](/guide/writing/mdc) to discover the full power of Markdown with Vue components.

## Thank you

We are thankful for all the contributions we received in Content v1 and are impatient to see what you will build with Nuxt 3 and Content v2 :blush:

::alert
The repository is open source under the MIT license and available on GitHub: [nuxt/content](https://github.com/nuxt/content)
::
