# Rascunho do artigo (formato ICML)

`main.tex` no formato do ICML (`icml2026.sty`; a folha de 2027 ainda nao foi publicada).
Nada aqui calcula metrica: as cinco tabelas e a figura saem de `runs/` pelos scripts do projeto,
de modo que nenhum numero do texto pode divergir da rodada que o produziu.

## O que nao esta versionado

- `main.pdf` e os auxiliares do LaTeX — recompilaveis.
- `figures/` — a figura de exemplos traz tracos de gravacoes que nao sao nossas para
  redistribuir.
- `style/` — os arquivos baixados do ICML; os `.sty`/`.bst` em uso estao nesta pasta.

## Reconstruir e compilar

```powershell
.venv\Scripts\python scripts\x3_paper_tables.py
.venv\Scripts\python scripts\x6_paper_figure.py
```

```powershell
cd paper; pdflatex main; bibtex main; pdflatex main; pdflatex main
```

A versao identificada, para circular entre os autores, sai do mesmo fonte:

```powershell
cd paper; pdflatex main-authors; bibtex main-authors; pdflatex main-authors; pdflatex main-authors
```

## As duas compilacoes

`main.tex` e o unico fonte. `main-authors.tex` define `\PDMIDENTIFIED` e o le, o que troca
`\usepackage{icml2026}` por `\usepackage[preprint]{icml2026}`: o bloco de autores aparece, o
agradecimento entra e o rodape diz `Draft of <data> -- not submitted`, sem afirmar nada sobre
aceite. Sem essa opcao a propria folha do ICML substitui os nomes por "Anonymous Authors" e as
filiacoes por "Anonymous Institution" -- nenhum nome e composto no PDF anonimo, de modo que nao
ha duas versoes do texto para manter em sincronia. `main-authors.pdf` nao se submete.

A lista de autores e a ordem foram trazidas do camera-ready do VISAPP 2027; a autoria deste
estudo ainda precisa ser confirmada, e o agradecimento carrega os dois numeros que aquele artigo
tambem deixou em aberto (o processo do PDSE e o projeto do Angel). Os tres pontos estao marcados
no `main.tex` com `[AUTHOR VERIFICATION REQUIRED]`.

## Como o artigo anterior e citado

O short paper do VISAPP 2027 entra em terceira pessoa, com a autoria real, o que o duplo-cego
do ICML permite para trabalho anterior. As duas passagens que o citam -- a seccao 1 e o
paragrafo "Reference cohort" da seccao 6 -- ja estavam escritas assim, de modo que nada muda
no camera-ready. A submissao em si continua anonima.
