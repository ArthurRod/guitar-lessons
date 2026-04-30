# Guitar Lessons — Visão Geral do Projeto

## Visão geral

Site de aulas de violão com foco em música worship, voltado para iniciantes. Conteúdo público, 100% estático, gerado com Astro 5. O roadmap contempla 8 aulas; aulas não publicadas aparecem como "em breve" na home.

- **Domínio:** https://guitar-lessons.arcawave.dev
- **Hospedagem:** GitHub Pages (deploy via `gh-pages`)
- **Template base:** ArthurRod/arcawave-blog

## Stack

| Camada | Tecnologia |
|---|---|
| Framework | Astro 5 |
| UI interativa | Svelte 5 |
| Conteúdo | MDX (`.mdx`) |
| Busca | Fuse.js (client-side) |
| SEO/Feed | @astrojs/sitemap + @astrojs/rss |
| Fonte | BDO Grotesk (arquivos em `public/fonts/`) |
| Deploy | gh-pages v6 |

## Estrutura de pastas

```
guitar-lessons/
├── public/
│   ├── CNAME                     # guitar-lessons.arcawave.dev
│   ├── robots.txt                # aponta sitemap
│   ├── fonts/                    # BDO Grotesk (Light → Black)
│   ├── ico/favicon.ico
│   ├── jpg/                      # hero images das aulas e páginas
│   └── png/                      # logo.png, og-logo.png
│
├── src/
│   ├── consts.ts                 # SITE_TITLE, SITE_DESCRIPTION, etc.
│   ├── content.config.ts         # schema da coleção blog (Zod)
│   ├── content/
│   │   └── blog/                 # arquivos .mdx de cada aula
│   │       └── aula-1-primeiro-contato.mdx
│   ├── layouts/
│   │   └── BlogPost.astro        # layout padrão para posts/aulas
│   ├── components/
│   │   ├── BaseHead.astro        # SEO, OG, preload de fonte
│   │   ├── Header.astro          # nav sticky com busca
│   │   ├── Footer.astro          # links de navegação e recursos
│   │   ├── HeaderLink.astro
│   │   ├── FormattedDate.astro   # data em pt-BR
│   │   ├── MenuMobile.astro
│   │   ├── SearchPosts.astro
│   │   └── svelte/
│   │       ├── Loading.svelte
│   │       ├── MenuMobile.svelte # hambúrguer responsivo
│   │       └── SearchPosts.svelte # busca client-side com Fuse.js
│   ├── pages/
│   │   ├── index.astro           # home: hero, últimas aulas, timeline
│   │   ├── about.astro           # página Sobre
│   │   ├── search.astro          # página de busca
│   │   ├── politicas-de-privacidade.astro
│   │   ├── 404.astro
│   │   ├── posts/[...slug].astro # renderiza cada aula
│   │   └── rss.xml.js            # feed RSS
│   └── styles/
│       ├── global.css            # design tokens + componentes globais
│       ├── header.css
│       ├── footer.css
│       ├── home.css
│       ├── post.css
│       ├── search.css
│       └── not-found.css
│
├── astro.config.mjs              # site, integrações (mdx, sitemap, svelte)
├── package.json
└── PROJECT_OVERVIEW.md           # este arquivo
```

## Como adicionar uma nova aula

### 1. Crie o arquivo MDX

```
src/content/blog/aula-2-trocas-e-ritmo.mdx
```

O slug do arquivo deve ser **idêntico** à entrada correspondente no array `roadmap` de [src/pages/index.astro](src/pages/index.astro) para que a aula apareça como publicada na timeline.

### 2. Frontmatter obrigatório/opcional

```mdx
---
title: "Aula 2 — Trocas suaves de acordes + ritmo na batida"
description: "Aprenda a trocar acordes com fluidez e domine a batida básica."
author: "Arca Wave"          # opcional
tags: "violão, aula 2, ..."  # opcional, string simples
pubDate: "May 07 2026"       # opcional; se omitido, não exibe data
heroImage: "/jpg/aula-2-hero.jpg"  # opcional
---
```

### 3. Adicione a imagem hero

Coloque o arquivo em `public/jpg/aula-2-hero.jpg` (720×360 px recomendado).

### 4. Verifique o roadmap

O roadmap em [src/pages/index.astro](src/pages/index.astro) já tem a entrada:

```js
{n: 2, slug: "aula-2-trocas-e-ritmo", title: "Trocas suaves de acordes + ritmo na batida", tag: "Iniciante"},
```

Assim que o arquivo MDX existir com esse slug, a aula deixa de aparecer como "em breve" e passa a ser clicável.

## Como rodar, buildar e fazer deploy

```bash
# Instalar dependências (uma vez)
npm install

# Servidor local com hot-reload
npm run dev
# → http://localhost:4321

# Build de produção (gera /dist)
npm run build

# Pré-visualizar o build localmente
npm run preview

# Deploy para GitHub Pages
npm run deploy
```

## Convenções de design

### Tokens CSS (definidos em `global.css`)

| Variável | Valor | Uso |
|---|---|---|
| `--primary` | `#f97316` | laranja — botões, destaques |
| `--primary-dark` | `#c2410c` | hover, links |
| `--secondary` | `#14b8a6` | teal — badges, callout goal |
| `--cream` | `#fff7ed` | fundo principal |
| `--cream-2` | `#ffedd5` | fundo de cards, code |
| `--black` | `#1f1a17` | texto principal |
| `--gray` | `#8a857f` | texto secundário |

Fonte: **BDO Grotesk** em 7 pesos (300 → 900), declarada via `@font-face` no `global.css`.

### Componentes interativos (usáveis dentro dos MDX)

#### `chord-grid` / `chord-card`
Grid responsivo de diagramas de acorde:
```html
<div class="chord-grid">
  <div class="chord-card">
    <span class="name">D</span>
    <div>Ré maior</div>
    <div class="label">base / casa</div>
  </div>
</div>
```

#### `strum`
Padrão visual de batida com setas:
```html
<div class="strum" aria-label="Descrição acessível do padrão">
  <span>↓</span><span>↓</span><span>↑</span><span>↑</span><span>↓</span><span>↑</span>
</div>
```

#### Callouts (`.callout`)
Três variantes de caixa de destaque:
```html
<div class="callout tip">   <!-- laranja — dica prática -->
<div class="callout goal">  <!-- teal — objetivos da aula -->
<div class="callout task">  <!-- roxo — tarefa da semana -->
```

#### `timeline` (home apenas)
Gerada automaticamente em `index.astro` a partir do array `roadmap`. Não é necessário editá-la manualmente; basta publicar o MDX com o slug correto.

## Roadmap de aulas

| # | Slug | Título | Status |
|---|---|---|---|
| 1 | `aula-1-primeiro-contato` | Primeiro contato com o violão + primeira música | ✅ Publicada |
| 2 | `aula-2-trocas-e-ritmo` | Trocas suaves de acordes + ritmo na batida | 🔒 Em breve |
| 3 | `aula-3-mais-acordes` | Novos acordes: Em, C e Bm (pestana leve) | 🔒 Em breve |
| 4 | `aula-4-graus-na-pratica` | Graus 1, 4, 5 e 6 — pensando como músico | 🔒 Em breve |
| 5 | `aula-5-segunda-musica` | Segunda música worship completa | 🔒 Em breve |
| 6 | `aula-6-batidas` | Variações de batida e dinâmica | 🔒 Em breve |
| 7 | `aula-7-tom-e-cifra` | Como ler cifra e mudar de tom | 🔒 Em breve |
| 8 | `aula-8-dedilhado` | Introdução ao dedilhado | 🔒 Em breve |
