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
fonte: "Rui Barbosa, Oração aos Moços, 1921"
resumo: "Uma linha que aparece na home."
description: "Uma frase para busca e para redes sociais."
autores: ["Rui Barbosa"]
temas: ["estudo", "método"]
---

Texto em Markdown.
```

`fonte:` credita a origem no cabeçalho do texto. Só faz sentido quando há trecho
de outro autor; num texto inteiramente seu, omita.

### Quem fala onde

Não há categoria separando "texto meu" de "texto dos outros". Houve, e foi
retirada: quase todo texto aqui é trecho alheio com comentário meu, e a linha
entre uma coisa e outra é tênue demais para virar arrumação. Quem resolve o
"mistura texto meu com texto dos outros" são três coisas dentro da própria
página:

- `fonte:` no cabeçalho, dizendo de quem é o trecho;
- a citação em bloco (`>`), que é do outro autor;
- a caixa de Nota, onde entra o comentário seu:

```markdown
<div class="comentario" markdown="1">

O que você tem a dizer sobre o trecho.

<p class="datacao">Origem, grifos, data da nota.</p>

</div>
```

### Autores e temas

`autores:` e `temas:` alimentam a página `/grafo/`. **Texto sem esses campos não
aparece ligado a nada.** Temas em uso: `ciência`, `estudo`, `mediunidade`,
`método`, `moral`, `política`. Autor só vira nó no grafo quando aparece em dois
ou mais textos.

### Destacar um trecho dentro da citação

Negrito não serve para isso. Dentro do trecho citado o texto já é itálico e já
está apagado em cinza, então o negrito mexe numa variável só e some. Para chamar
o olho do leitor a uma passagem, use `<mark>`:

```markdown
> <mark>A frase que você quer que o leitor não perca.</mark> O resto do
> parágrafo segue normalmente.
```

O trecho marcado sai do cinza e sobe para o branco do texto corrido, com um
filete fino por baixo. O destaque não acrescenta nada à página: ele apenas
deixa de apagar o que estava apagado.

`<mark>` é a marcação certa também fora do visual: leitor de tela anuncia como
realce, e o RSS carrega junto. Fora de citação o efeito é mais fraco, porque ali
o texto já está claro e sobra só o filete.

**Um por texto.** Ele é forte de propósito; havendo dois, deixa de destacar.
É limite próprio, separado dos dois grifos em negrito.

**Sempre declarar**, como qualquer grifo acrescentado, na linha de datação:

```html
<p class="datacao">O destaque no terceiro parágrafo é meu.</p>
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

**Autor morto há mais de 70 anos:** domínio público. Reproduza à vontade.

**Autor vivo ou morto há menos de 70 anos:** trecho + comentário seu, com autor e
origem indicados (LDA 9.610/98, art. 46, III). Texto integral, só com autorização
por escrito — e guarde o e-mail.

Atenção às **traduções**: o prazo conta a partir da morte do tradutor, não do autor.
Um original em domínio público pode ter tradução protegida.

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
