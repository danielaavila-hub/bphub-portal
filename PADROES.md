# PADROES.md — Convenções do Portal BPHUB

> **Para o Claude:** leia este arquivo inteiro antes de criar ou editar qualquer material do portal.
> Ele complementa o skill "produtor-de-materiais" com decisões mais recentes. Em caso de
> conflito entre o skill e este arquivo, **este arquivo vence**.
>
> Última atualização: julho de 2026.

## Publicação

- O repositório do portal é **`danielaavila-hub/bphub-portal`** (GitHub Pages → `portal.brazilianportuguesehub.com`).
  **Não** usar os repositórios `exercicios-bph`, `Brazilian-Portuguese-Hub` ou similares — são antigos.
- A pasta `bphub-portal/` dentro do repositório é um duplicado legado — **ignorar**. Os arquivos ativos
  ficam em `exercicios/`, `a1/` … `c2/` na raiz.
- Exercícios ficam em `exercicios/`, com nome `tema-nivel-exercicios-aluno.html` (e `-material.html` ou
  `-referencia.html` para o material de referência, quando houver).
- **Nunca gerar guia da professora.**
- Ao alterar mais de um arquivo (ex.: exercício + índice do nível), fazer **um commit único** via
  Git Data API (blobs → tree → commit → ref). Commits em sequência rápida disparam deploys
  concorrentes do Pages, que falham e geram emails de erro.
- Depois de publicar, conferir o build (`GET /pages/builds/latest`) e a página no ar. Se o build
  travar ou falhar, reenfileirar com `POST /pages/builds`.
- Todo material novo ganha **card no índice do nível** (`a1/index.html` etc.): `data-order` sequencial,
  `data-tags` (gram/func/tema/gen/cult/fon), `data-search` rico em palavras-chave, data "Added Mês Ano".
  Os contadores da página se atualizam sozinhos via JS.
- Antes de criar um material de uma série existente (ex.: Língua da Gente), **baixar um arquivo recente
  da mesma série e nível como modelo exato** de estrutura, CSS e JS.

## Hero e layout

- Tradução ou subtítulo do título: **em bloco abaixo do h1**, itálico, cor ouro (`var(--ouro)` #FFB94A),
  `font-size: 0.72em`, `margin-top: 4px`. CSS: `.hero h1 em { display: block; font-style: italic;
  color: var(--ouro); font-size: 0.72em; margin-top: 4px; }`
- Conteúdo centralizado: `.main { max-width: 920px; margin: 0 auto; }`. Topbar e hero ficam de
  ponta a ponta (não centralizar).
- **Não usar** a nota "📝 Complete após a aula" (abolida em julho/2026).
- Eyebrow do hero é sempre "Materials Portal". Cores por nível conforme o skill
  (A1 #4E551D · A2 #265B8B · B1 #967E63 · B2 #D36D29 · C1 #A1441D · C2 #1E1D1C).

## Línguas por nível

- A1–B1: instruções e hero-sub em **inglês**; todo o conteúdo em português. Não misturar as duas
  línguas na mesma frase.
- B2: tudo em português; permitidas apenas glosas inglesas inline de exemplos, entre parênteses,
  em cinza (`color:#999`).
- C1–C2: tudo em português, sem exceção.

## Exercícios interativos

- Todo exercício fechado tem botão **"✓ Check answers"** que mostra a nota **e o gabarito completo**
  listado item por item (✓/✗ + resposta modelo), em painel rolável (`max-height: 260px; overflow-y: auto`).
- Exercícios de **interpretação de texto** também têm check: correção por palavras-chave
  (função `norm()` tolerante a acentos) + resposta modelo exibida.
- Em **multiple choice**, a opção clicada precisa ficar visivelmente marcada (classe `.selected`
  com borda/fundo cobalto) antes da correção.
- Se o enunciado pede **expressão + verbo**, mostrar a expressão **entre colchetes** no fim da frase
  (ex.: `[dever]`), em cobalto; placeholder genérico ("...") que não entrega a resposta.
- Placeholders nunca revelam o início da resposta. Produção livre: "Escreva sua resposta aqui...".
- Respostas modelo mostram **apenas a forma correta** — não listar variantes duvidosas
  (ex.: sujeito duplicado "A Beatriz ela mesma..." não entra no gabarito).

## Regras linguísticas e pedagógicas

- **Verbos dêiticos (levar/trazer, ir/vir, pegar):** todo item de exercício declara **onde o falante
  está** — etiqueta de contexto no enunciado (ex.: `[Você está na festa.]`, estilo Via Brasil) ou
  âncoras dêiticas na própria frase (aqui, pra cá, aí, no caminho, de volta). Nunca deixar item com
  duas respostas defensáveis. Em textos (diálogos, WhatsApp), deixar claro onde cada personagem está
  (nota cultural ou na própria fala).
- **Futuro do subjuntivo:** não ensinar como "verbos irregulares". Ensinar a regra única: forma
  *eles* do pretérito perfeito menos **-am** (eles tiveram → tiver; eles foram → for). A
  irregularidade está no perfeito, não no futuro do subjuntivo.
- Exemplos dos painéis de gramática devem **citar frases do texto do material** — se o texto mudar,
  atualizar os exemplos junto.
- Locuções prepositivas e expressões apresentadas em lista levam **tradução inglesa** entre
  parênteses, em cinza (até B2).
- Textos autênticos sempre com fonte citada (padrão do skill). Agência Brasil/Agência Gov:
  "Reprodução gratuita mediante citação da fonte."

## Músicas — seção "Sons do Brasil"

- Materiais baseados em música **não vão nos índices de nível** (a1/…/c2). Eles ficam na seção
  própria **`musicas/index.html`** ("Sons do Brasil"), organizada por gênero musical
  (MPB, Samba & Bossa Nova, Forró, Axé, Rock, Funk, Gospel, Sertanejo…).
- Nome do arquivo: **`musica-<titulo>-<artista>-exercicios-aluno.html`** em `exercicios/`
  (ex.: `musica-garota-de-ipanema-`, `musica-brasil-cazuza-`).
- O card usa o formato **`mus-card`** próprio da seção (não `mat-card`): barra na cor do gênero
  (`var(--samba)`, `var(--mpb)`…), badge de nível com o hex do nível, linha do artista, tags de
  gênero/foco, e "Open material →". **Atualizar o contador** `genre-count` da seção manualmente.
- O topbar do exercício leva o link **"← Músicas"** para `../musicas/index.html`.
- **Direitos autorais:** nunca reproduzir a letra completa. Embutir o vídeo/gravação oficial
  (YouTube embed) para a escuta e citar apenas trechos curtos nos exercícios, com fonte
  (`Autor, "Título" (ano) · Gravação: intérprete`) e a nota "Trechos citados apenas para fins didáticos".

## Envio de respostas

- O envio é feito via **Brevo** (não mais Formspree — o skill está desatualizado neste ponto).
  Copiar o bloco `bphubSubmit()` de um arquivo recente que já usa Brevo, ex.:
  `exercicios/transito-a2-exercicios-aluno.html` ou `exercicios/lingua-da-gente-b1-ipad-exercicios-aluno.html`.
- O bloco Brevo envia: (1) email com todas as respostas para daniela.avila@brazilianportuguesehub.com
  e (2) cópia por template para o email do aluno, se preenchido. Coletar TODAS as respostas do
  material no payload (inputs, selects, botões e textareas), não apenas textareas.
- Formulário padrão no final de todo `*-exercicios-aluno.html`; após envio, mostrar resumo das
  respostas na tela e marcar o material como concluído via `localStorage` (`bphub_done_<slug>`).
- Material avulso (sem par referência/exercícios) **não** leva nav-link.
