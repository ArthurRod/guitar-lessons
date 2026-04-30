# Guitar Lessons 🎸

Blog de aulas de violão com foco em música worship — toque desde a primeira aula.
Construído com [Astro](https://astro.build) + [Svelte](https://svelte.dev), publicado via GitHub Pages no domínio **guitar-lessons.arcawave.dev**.

> Estrutura inspirada em [`ArthurRod/arcawave-blog`](https://github.com/ArthurRod/arcawave-blog).

## 🚀 Comandos

| Comando             | Ação                                   |
| ------------------- | -------------------------------------- |
| `npm install`       | Instala dependências                   |
| `npm run dev`       | Servidor local em `localhost:4321`     |
| `npm run build`     | Build de produção em `./dist/`         |
| `npm run preview`   | Pré-visualiza o build                  |
| `npm run deploy`    | Publica `./dist/` no GitHub Pages      |

## 🌐 Domínio

O arquivo [`public/CNAME`](./public/CNAME) já contém `guitar-lessons.arcawave.dev`.
Configure o DNS apontando o subdomínio para o GitHub Pages
(`<seu-usuario>.github.io`) e habilite Pages em **Settings → Pages → Source: gh-pages branch**.

## ✍️ Adicionar uma nova aula

Crie um arquivo `.md` ou `.mdx` em `src/content/blog/` seguindo o frontmatter:

```yaml
---
title: "Aula 2 — ..."
description: "..."
author: "Arca Wave"
tags: "violão, aula 2, ..."
pubDate: "May 07 2026"
heroImage: "/jpg/aula-2-hero.jpg"
---
```

Depois é só dar `npm run build && npm run deploy`.

## 🎨 Design

Paleta amigável: laranja quente (`#f97316`) + teal (`#14b8a6`) sobre creme (`#fff7ed`).
Fonte: **BDO Grotesk** (em `public/fonts/`).
Mobile-first.
