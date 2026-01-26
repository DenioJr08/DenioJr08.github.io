# Instruções rápidas para Jekyll (para iniciantes)

Este documento explica, de forma prática e direta, como configurar, desenvolver e publicar um blog profissional usando Jekyll no Windows. O conteúdo do blog e o tema podem ser definidos depois — aqui foco nas funcionalidades e fluxo de trabalho.

## 1. Objetivo
- Criar um blog estático com estrutura profissional, SEO, feed, e deploy automatizado.

## 2. Pré-requisitos (Windows)
- Ruby (recomendado: RubyInstaller + MSYS2)
- Git
- Editor de texto (VS Code recomendado)

## 3. Instalação rápida (Windows)
1. Instale o Ruby via RubyInstaller: https://rubyinstaller.org/ (escolha versão compatível com Jekyll, geralmente 3.x ou 2.7+).
2. No instalador, marque a opção para instalar MSYS2 e as dev tools.
3. Abra o `Start Command Prompt with Ruby` (ou use PowerShell se tiver path configurado).

Comandos básicos:

```bash
# instalar bundler (uma vez)
gem install bundler

# no diretório do projeto, instalar gems do Gemfile
bundle install

# servir localmente com live reload
bundle exec jekyll serve --livereload

# gerar site estático apenas (build)
bundle exec jekyll build
```

Se não tiver `Gemfile`, crie um com pelo menos:

```ruby
source 'https://rubygems.org'
gem 'jekyll', '~> 4.3'
gem 'minima'
gem 'jekyll-feed'
gem 'jekyll-seo-tag'
gem 'jekyll-sitemap'
```

Depois rode `bundle install`.

## 4. Estrutura detalhada de pastas e arquivos
Este tópico descreve as pastas mais comuns em um site Jekyll e que tipo de arquivo colocar em cada uma.

- `/_posts/` — posts do blog em Markdown ou HTML; nome no formato `YYYY-MM-DD-slug.md`.
  - Conteúdo: artigos com front matter YAML (title, date, layout, tags, categories, summary, image, etc.).

- `/_drafts/` — posts em andamento (sem data). Útil para rascunhos; publique movendo para `_posts/` com data.

- `/_layouts/` — templates de página em HTML+Liquid (por ex. `default.html`, `post.html`, `home.html`). Layouts controlam o HTML principal e onde o `{{ content }}` é inserido.

- `/_includes/` — fragmentos reutilizáveis (header, footer, nav, post-card, social-links). Inclua com `{% include header.html %}`.

- `/_data/` — arquivos de dados em YAML/JSON/CSV (ex.: `authors.yml`, `navigation.yml`) usados via `site.data.nome`.

- `/_sass/` — partials SCSS (`_variables.scss`, `_mixins.scss`) compilados em CSS via `assets` ou `css` pipeline.

- `/assets/` — recursos públicos: `css/`, `js/`, `images/`, fontes. Estruture como `assets/images/`, `assets/css/`.
  - Coloque imagens otimizadas, arquivos estáticos e arquivos gerados por ferramentas de bundling.

- `/pages/` ou raiz (p. ex. `about.md`, `contact.md`) — páginas estáticas com front matter (layout: page).

- `/_site/` — pasta gerada pelo Jekyll após `jekyll build` (output). Não commite essa pasta no git.

- `Gemfile` — lista de gems (jekyll, plugins, tema). Use `bundle install` para gerenciar dependências.

- `_config.yml` — arquivo central de configuração (title, url, baseurl, plugins, permalink, defaults).

- `.gitignore` — inclua `_site/`, `.sass-cache/`, `.jekyll-cache/`, `node_modules/` (se usar), arquivos sensíveis.

- `CNAME` (opcional) — nome de domínio personalizado para GitHub Pages.

- `robots.txt`, `favicon.ico`, `manifest.json` — arquivos estáticos na raiz, se necessários.

Observações rápidas:
- Tipos de arquivo: posts → `.md` (Markdown) ou `.html`; layouts/includes → `.html`; dados → `.yml`/`.json`.
- Use front matter consistente nos posts (title, date, tags, categories, summary, image) para facilitar templates e SEO.

## 5. Exemplos de conteúdo por pasta
- `_posts/` — `2026-01-22-primeiro-post.md` (Markdown com front matter YAML).
- `_includes/` — `header.html`, `footer.html`, `post-card.html`.
- `_layouts/` — `default.html` (estrutura), `post.html` (article markup), `home.html`.
- `_data/` — `authors.yml`:

```yaml
denio:
  name: "Denio"
  bio: "Desenvolvedor e escritor"
  avatar: /assets/images/denio.jpg
```

## 6. Front matter recomendado (exemplo)
Use um conjunto padrão para facilitar templates e SEO:

```yaml
---
title: "Título do post"
date: 2026-01-22 10:00:00 -0300
layout: post
categories: [categoria]
tags: [tag1, tag2]
summary: "Resumo curto para listagens e meta description"
image: /assets/images/cover.jpg
author: denio
draft: false
---
```

## 7. Boas práticas e recomendações para um blog profissional
Organizei por categoria para facilitar a aplicação.

- Conteúdo e arquitetura editorial:
  - Planeje um calendário editorial e mantenha consistência de publicação.
  - Use categorias para seções amplas e tags para temas específicos; não exagere no número de categorias.
  - Crie templates para diferentes tipos de conteúdo (artigo, tutorial, série, nota rápida).
  - Escreva meta descriptions curtas (120–160 chars) e títulos claros.

- SEO e metadados:
  - Instale `jekyll-seo-tag` e preencha `title`, `description`, `url`, `twitter_username`, `github_username` em `_config.yml`.
  - Use imagens sociais (`og:image`) e inclua alt text em imagens.
  - Gere `sitemap.xml` (`jekyll-sitemap`) e `feed.xml` (`jekyll-feed`).
  - Configure URLs canônicas e `rel="canonical"` quando necessário.

- Performance e imagens:
  - Otimize imagens antes de commitar (WebP, múltiplas resoluções). Use `jekyll-picture-tag` para responsive images.
  - Use `loading="lazy"` em imagens fora do viewport inicial.
  - Minifique CSS/JS e agrupe assets críticos no cabeçalho para reduzir tempo de render.

- Acessibilidade (a11y):
  - Use tags semânticas (`<main>`, `<article>`, `<nav>`, `<header>`).
  - Mantenha contraste suficiente e teste navegação por teclado.
  - Sempre forneça `alt` em imagens e labels em formulários.

- UX e design:
  - Tipografia: escolha fontes legíveis e tamanhos adequados para leitura em mobile.
  - Navegação clara: menu principal, busca (se possível), e breadcrumbs quando útil.
  - Páginas “sobre” e “contato” claras, com informações de autor e políticas (privacidade, cookies).

- Código e destaque de sintaxe:
  - Use `rouge` (padrão) para highlight; especifique `highlighter: rouge` no `_config.yml`.
  - Mostre linguagem no bloco de código (```ruby). Considere tema com contraste para código.

- Analytics, comentários e privacidade:
  - Use Google Analytics 4 ou alternativas (Plausible, Fathom) dependendo de privacidade.
  - Para comentários, escolha entre Disqus (rápido) ou soluções abertas (Staticman) com moderação.
  - Informe sobre cookies e respeite leis de privacidade conforme seu público.

- Automação e manutenção:
  - Automatize builds e deploys (Actions, Netlify, Vercel) — embora tenhamos pulado detalhes de CI aqui.
  - Mantenha gems atualizadas (`bundle update`) e revise plugins antes de instalar.

- Segurança e versão:
  - Nunca coloque segredos no repositório (tokens, senhas). Use GitHub Secrets para CI.
  - Faça backups via repositório remoto e tags/releases para versões importantes.

- Testes e verificação:
  - Use `htmlproofer` (em um job de CI) para checar links quebrados e acessibilidade básica.
  - Verifique performance com Lighthouse e corrija problemas críticos.

## 8. Passo-a-passo prático para criar um blog profissional (resumido)
1. Atualize `_config.yml` com `title`, `description`, `url`, `baseurl`, `theme` e plugins essenciais (`jekyll-seo-tag`, `jekyll-sitemap`, `jekyll-feed`).
2. Escolha um tema ou crie `/_layouts/default.html` e `/_layouts/post.html` personalizados.
3. Crie includes reutilizáveis (`_includes/header.html`, `_includes/footer.html`, `_includes/post-card.html`).
4. Estruture `assets/` com `css/`, `js/` e `images/`; adicione variáveis SCSS em `/_sass/`.
5. Crie `_data/authors.yml` para gerenciar perfis de autores.
6. Escreva o primeiro post em `_posts/` com front matter completo e imagem social.
7. Teste localmente: `bundle exec jekyll serve --livereload` e verifique desktop e mobile.
8. Otimize imagens e verifique SEO (títulos, descrições, open graph).
9. Configure analytics e uma política de privacidade simples.
10. Faça commits pequenos e mantenha histórico claro (branch para features, tags para releases).

## 9. Checklist rápido antes de publicar
- Título e meta description preenchidos.
- Imagem social (`og:image`) funcionando.
- Links internos e externos testados.
- Imagens otimizadas e com `alt`.
- Responsividade e leitura em dispositivos móveis verificados.
- Analytics configurado e funcionando.

---
Se quiser, aplico essas recomendações no projeto agora: por exemplo, gerar um `Gemfile` com os plugins listados, criar `/_includes/` básicos e um layout `post.html` minimal. Informe quais itens quer que eu crie primeiro.


## 5. Como escrever um post (front matter)
Crie um arquivo em `_posts/2026-01-22-meu-post.md` com topo YAML:

```yaml
---
title: "Título do post"
date: 2026-01-22 10:00:00 -0300
categories: [categoria]
tags: [tag1, tag2]
layout: post
summary: "Resumo curto para listagens e meta description"
image: /assets/images/cover.jpg
---

Conteúdo em Markdown aqui...
```

Dicas:
- Use `summary` para controle manual do trecho mostrado em listagens.
- Use `permalink` em `_config.yml` para formatar URLs: ex: `permalink: /:categories/:year/:month/:day/:title/`.

## 6. Configurações recomendadas em `_config.yml`

Exemplo mínimo:

```yaml
title: Meu Blog Profissional
email: seu@exemplo.com
description: "Pequena descrição para meta"
baseurl: "" # ou /seusite
url: "https://seu-dominio.com"
theme: minima
plugins:
  - jekyll-feed
  - jekyll-seo-tag
  - jekyll-sitemap
```

Ative `jekyll-seo-tag` no layout `<head>` com `{{ site | seo }}` (ou use o include recomendado pelo plugin).

## 7. Recursos profissionais e plugins úteis
- `jekyll-seo-tag`: metas SEO automáticas.
- `jekyll-sitemap`: gera `sitemap.xml`.
- `jekyll-feed`: gera `feed.xml` (RSS/Atom).
- `jekyll-paginate-v2`: paginação avançada.
- `jekyll-assets` ou `jekyll-picture-tag`: otimização de imagens e responsive images.

Instale adicionando ao `Gemfile` e ao `_config.yml` conforme a documentação de cada plugin.

## 8. Testar localmente e fluxo de edição
- Para desenvolver: rode `bundle exec jekyll serve --livereload` e acesse `http://127.0.0.1:4000`.
- Quando alterar `_config.yml`, reinicie o servidor.

## 9. Controle de versão e boas práticas
- Use Git com commits pequenos e descritivos.
- Ignore `_site/`, `.sass-cache/`, `.jekyll-cache/` no `.gitignore`.
- Mantenha imagens em `assets/images` e otimize antes de commitar.

## 10. Deploy — GitHub Pages (simples)
Opção A — usar GitHub Pages (build pelo GitHub):
- Nomeie o repositório `username.github.io` para publicar na raiz ou use branch `gh-pages`/`gh-pages` ou `main` com /docs.
- Se usar gems que o GitHub Pages não suporta, escolha build via Actions (recomendado para plugins modernos).

Opção B — usar GitHub Actions (recomendado para controle total):

Exemplo mínimo de workflow (salve em `.github/workflows/jekyll-deploy.yml`):

```yaml
name: build and deploy Jekyll site

on:
  push:
    branches: [ main ]

jobs:
  build-deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - name: Setup Ruby
        uses: ruby/setup-ruby@v1
        with:
          ruby-version: '3.1'
      - name: Install dependencies
        run: |
          gem install bundler
          bundle install
      - name: Build site
        run: bundle exec jekyll build --destination public
      - name: Deploy to GitHub Pages
        uses: peaceiris/actions-gh-pages@v3
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          publish_dir: ./public
```

Essa ação gera o site e publica em `gh-pages` por padrão; configure no repositório o GitHub Pages apontando para a branch `gh-pages` (ou configure a action para outra branch).

## 11. SEO, Analytics e comentários
- SEO: `jekyll-seo-tag` + meta `og` images definidas por post.
- Analytics: adicione o script do Google Analytics no `_includes/head.html` (ou use plugin oficial para Jekyll se preferir).
- Comentários: Disqus (fácil) ou soluções sem servidor como Staticman (mais trabalho).

## 12. Performance e Acessibilidade
- Otimize imagens (webp, múltiplas resoluções).
- Use `lazy loading` para imagens (`loading="lazy"`).
- Teste contraste de cores e navegação por teclado.

## 13. Backups e ambiente de produção
- Tenha o repositório no GitHub (ou outro remote).
- Faça releases/tags para versões importantes do site.

## 14. Próximos passos sugeridos
1. Personalizar `title`, `description` e `url` em `_config.yml`.
2. Escolher tema ou criar layouts customizados em `_layouts/`.
3. Adicionar plugins desejados ao `Gemfile` e rodar `bundle install`.
4. Criar o primeiro post em `_posts/` e testar `bundle exec jekyll serve`.
5. Configurar CI/CD com o workflow acima para deploy automático.

---
Se quiser, posso:
- gerar um `Gemfile` pronto para este projeto;
- criar um workflow de GitHub Actions já configurado no repositório;
- ou adaptar `JEKYLL_INSTRUCTIONS.md` com exemplos específicos do seu tema preferido.

Arquivo criado: `JEKYLL_INSTRUCTIONS.md` (na raiz do projeto).
l