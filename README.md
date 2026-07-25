# Singelas Referências

Site estático (Jekyll) para GitHub Pages. Sem tema de terceiro. Os dois únicos
plugins, `jekyll-feed` e `jekyll-sitemap`, rodam na compilação e geram um arquivo
cada, o `feed.xml` e o `sitemap.xml`. Nada aqui precisa de atualização de segurança
porque nada aqui roda: o GitHub gera HTML no push e serve arquivo parado.

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

## Estatísticas

O GitHub Pages não informa nada sobre quem lê. Não há log de servidor, e o painel
do repositório conta visita ao código, não ao site. Os números vêm de dois lugares,
que respondem a perguntas diferentes:

**Search Console** (Google) e **Bing Webmaster Tools** dizem por quais buscas as
pessoas chegam, quantas vezes o site apareceu e o que foi indexado. Não exigem
nenhum código na página, só a prova de que o domínio é seu:

1. Em `search.google.com/search-console`, escolha **Domínio** e digite
   `singelasreferencias.com.br`.
2. Copie o registro TXT que ele mostrar.
3. No Registro.br, em **Editar zona DNS**, crie o TXT com esse valor.
4. Volte e confirme. A propagação leva de minutos a algumas horas.
5. Verificado, vá em **Sitemaps** e envie `sitemap.xml`.

O `sitemap.xml` é gerado pelo `jekyll-sitemap` a cada compilação, com todos os
textos. Ele não faz nada subir no ranking. Serve para entregar ao Google a lista
completa de endereços, o que torna útil o relatório de páginas do Search Console:
sem ela, não há com o que comparar o que foi indexado.

**GoatCounter** conta quantas vezes cada texto foi aberto. Gratuito para uso
pessoal, código aberto, uns 3 KB de script. Não grava cookie nem identificador,
e é por isso que o site não precisa de banner de consentimento:

1. Crie a conta em `goatcounter.com`, escolhendo um código de site.
2. Ponha esse código no `_config.yml`, em `goatcounter:`.
3. Push. O `_includes/analytics.html` cuida do resto.

Com `goatcounter:` vazio, nenhum script é carregado. O contador também não roda em
`jekyll serve` local, senão cada revisão sua entraria na conta como leitor.

Duas coisas que os números não mostram. **Quem lê pelo RSS nunca aparece**, porque
leitor de feed não executa JavaScript. E **os primeiros meses são ruído**: num site
com poucos textos, a variação semanal diz mais sobre o acaso de um link
compartilhado do que sobre o que está sendo lido.

## Assinatura por e-mail

O site é estático e não recebe cadastro: um formulário precisa de servidor para
gravar o endereço. Então a lista mora no **Buttondown**, que vigia o `feed.xml` e
dispara o e-mail quando aparece texto novo. Escrever e dar push continua sendo
tudo o que você faz.

1. Crie a conta em `buttondown.com` e anote o nome de usuário.
2. Ponha esse nome no `_config.yml`, em `buttondown:`.
3. Lá, em **Settings → RSS-to-email** (ou equivalente), aponte para
   `https://singelasreferencias.com.br/feed.xml`.
4. Configure SPF e DKIM no Registro.br com os valores que o Buttondown fornecer,
   para o e-mail sair como `@singelasreferencias.com.br` sem cair em spam. Sem
   isso, dá para começar remetendo pelo domínio deles.

Com `buttondown:` vazio, o formulário não aparece e o site fica como estava.

### O feed leva o resumo, não o texto

`excerpt_only: true` no `_config.yml`. O que vai é o `description:` do cabeçalho,
aquela frase que você já escreve à mão, mais o link.

O motivo é que o texto integral se desmancha fora da página. As notas de rodapé
viram `href="#fn:1"`, âncoras que só existem aqui e que, num e-mail, não levam a
lugar nenhum. E a caixa de comentário viaja sem o CSS, de modo que o comentário
seu e a citação do outro autor chegam como dois blocos iguais. Como é a página
que resolve o "quem fala onde", mandar o texto para fora dela é mandar a metade
que não se explica sozinha.

Isso vale também para quem lê por RSS, que perde o texto integral no leitor de
feed. É o preço da mesma escolha, e reverter é apagar uma linha.

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
_includes/analytics.html   contador de visitas, só em produção
_includes/inscrever.html   formulário da lista de e-mail
index.html                 lista da home
sobre.md                   a nota de autor, versão longa
assets/css/style.css       tudo — sem framework, sem build
_posts/                    os textos
```
