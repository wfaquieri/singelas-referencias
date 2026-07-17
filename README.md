# Singelas Referências

Site estático (Jekyll) para GitHub Pages. Sem tema de terceiro, sem plugin além do
`jekyll-feed`. Nada aqui precisa de atualização de segurança porque nada aqui roda:
o GitHub gera HTML no push e serve arquivo parado.

## Publicar

1. Criar um repositório **novo** no GitHub — não use `wfaquieri.github.io`, que é o CV.
   Sugestão de nome: `singelas-referencias`.

2. Na pasta deste projeto:

   ```
   git init
   git add .
   git commit -m "Primeiro commit"
   git branch -M main
   git remote add origin git@github.com:wfaquieri/singelas-referencias.git
   git push -u origin main
   ```

3. No GitHub: **Settings → Pages → Source: Deploy from a branch → main / (root)**.

4. Alguns minutos depois o site está no ar.

## Endereço

**Sem domínio próprio** — o site fica em `wfaquieri.github.io/singelas-referencias`.
Nesse caso, edite o `_config.yml`:

```yaml
url: "https://wfaquieri.github.io"
baseurl: "/singelas-referencias"
```

**Com domínio próprio** (recomendado — ~R$ 40/ano no Registro.br, e é a única
coisa que você leva embora se um dia mudar de plataforma):

1. Registre o domínio.
2. No Registro.br, aponte para o GitHub:
   - `A` → `185.199.108.153`, `185.199.109.153`, `185.199.110.153`, `185.199.111.153`
   - ou `CNAME` → `wfaquieri.github.io` (se for subdomínio, tipo `blog.seudominio.com.br`)
3. No GitHub: **Settings → Pages → Custom domain**, digite o domínio, salve e marque
   **Enforce HTTPS**.
4. No `_config.yml`:

   ```yaml
   url: "https://seudominio.com.br"
   baseurl: ""
   ```

Domínio próprio no GitHub Pages não custa nada além do registro. Ele também mantém
os ensaios separados do CV aos olhos do Google, que é o motivo de não jogar tudo
em `wfaquieri.github.io`.

## Escrever

Um arquivo em `_posts/`, no formato `AAAA-MM-DD-titulo-em-kebab-case.md`:

```markdown
---
layout: post
title: "Título do texto"
date: 2026-07-20
categories: referencias      # ou: apontamentos
resumo: "Uma linha que aparece na home."
---

Texto em Markdown.
```

### As duas categorias

- `apontamentos` — texto seu. Aparece rotulado como **Apontamento**.
- `referencias` — trecho de outro autor com o seu comentário. Rótulo: **Referência**.

É a distinção que resolve o "mistura texto meu com texto dos outros": ela fica
explícita no rótulo, e o leitor sabe sempre o que está recebendo. Para creditar a
origem no cabeçalho, use `fonte:` no front matter:

```yaml
fonte: "Rui Barbosa, Oração aos Moços, 1921"
```

### Notas de rodapé

Funcionam nativamente (kramdown). No corpo do texto:

```markdown
...conforme escreveu Kardec.[^1]

[^1]: Allan Kardec, *A Gênese*, cap. I, item 55.
```

Kramdown junta todas as notas no fim da página e cria o link de ida e volta. É o
motivo principal de este site não ser o Medium, que simplesmente não tem nota de
rodapé.

### Direito autoral

Autor morto há mais de 70 anos: domínio público, reproduza à vontade
(Rui Barbosa †1923, Victor Hugo †1885, Bach †1750).

Autor vivo — Alberto Oliva, por exemplo: **trecho + comentário seu**, com autor e
origem indicados (LDA 9.610/98, art. 46, III). Texto integral, só com autorização
por escrito.

## Rodar localmente (opcional)

Precisa de Ruby. Não é obrigatório — dá para escrever e dar push direto, e conferir
no ar em dois minutos.

```
bundle install
bundle exec jekyll serve
```

Depois: `http://localhost:4000`.

## Estrutura

```
_config.yml                título, tagline, rótulos, meses em português
_layouts/default.html      moldura do site
_layouts/post.html         página de texto + nota de autor no rodapé
index.html                 lista da home
sobre.md                   a nota de autor, versão longa
assets/css/style.css       tudo — sem framework, sem build
_posts/                    os textos
```
