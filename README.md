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

## Como o artigo anterior e citado

O short paper do VISAPP 2027 entra em terceira pessoa, com a autoria real, o que o duplo-cego
do ICML permite para trabalho anterior. As duas passagens que o citam -- a seccao 1 e o
paragrafo "Reference cohort" da seccao 6 -- ja estavam escritas assim, de modo que nada muda
no camera-ready. A submissao em si continua anonima (`\icmlauthor{Anonymous}`).
