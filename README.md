# When Does Encoding Dynamics as Colour Help?

Fonte LaTeX do artigo *"When Does Encoding Dynamics as Colour Help? Seven Handwriting Cohorts and
an Acquisition Floor"*, no formato do ICML (`icml2026.sty`; a folha de 2027 ainda nao foi
publicada).

Este repositorio e **privado** e esta sincronizado com o Overleaf, que e onde a prosa se edita a
varias maos. O estudo que produz os numeros vive noutro lugar: `PDM2`, o repositorio de pesquisa
(codigo, protocolos por base, rodadas). Aqui so entra o que o LaTeX precisa.

## Dois destinos, dois documentos

| arquivo | destino | formato |
|---|---|---|
| `main.tex` | ICML (conferencia) | folha do ICML, corpo em 8 paginas, duas colunas |
| `main-mdpi.tex` | **Applied Sciences** (MDPI), Special Issue *Statistics in Data Science* | formato livre, coluna unica, 16 paginas |

Os dois compartilham `tables/`, `figures/` e `main.bib`, e nenhum numero difere entre eles. O que
muda e a estrutura, que a revista fixa (Introduction, Materials and Methods, Results, Discussion,
Conclusions), o resumo, que a revista limita a cerca de 200 palavras contra as 498 da versao do
ICML, e o back matter obrigatorio.

A versao MDPI **nao usa o template da revista**, de proposito: a licenca do template diz que ele
"cannot be used for posting online on preprint servers or other websites", e este repositorio e
publico. A revista aceita *free format submission* -- "We do not have strict formatting
requirements, but all manuscripts must contain the required sections" -- e todas as secoes
exigidas estao la, na ordem dela. Na revisao, quando pedirem o template, troca-se.

```powershell
pdflatex main-mdpi; bibtex main-mdpi; pdflatex main-mdpi; pdflatex main-mdpi
```

## As duas compilacoes do documento do ICML

`main.tex` e o unico fonte. `main-authors.tex` define `\PDMIDENTIFIED` e o le, o que troca
`\usepackage{icml2026}` por `\usepackage[preprint]{icml2026}`: o bloco de autores aparece, o
agradecimento entra e o rodape diz `Draft of <data> -- not submitted`, sem afirmar nada sobre
aceite. Sem essa opcao a propria folha do ICML substitui os nomes por "Anonymous Authors" e as
filiacoes por "Anonymous Institution" -- nenhum nome e composto no PDF anonimo, de modo que nao
ha duas versoes do texto para manter em sincronia.

| arquivo | o que e | quando se usa |
|---|---|---|
| `main.tex` | build **cego**, sem autores | e este que se submete |
| `main-authors.tex` | build identificado | para ler e revisar entre nos |

No Overleaf, **defina `main-authors.tex` como documento principal**, para que o PDF que todos veem
traga os nomes. `main-authors.pdf` nao se submete.

```powershell
pdflatex main-authors; bibtex main-authors; pdflatex main-authors; pdflatex main-authors
```

## As tabelas e a figura sao geradas -- nao editar a mao

As sete tabelas em `tables/` e `figures/examples.png` saem de `runs/` no repositorio de pesquisa,
pelos scripts `x3_paper_tables.py` e `x6_paper_figure.py`. Nada aqui calcula metrica, e e assim de
proposito: nenhum numero do texto pode divergir da rodada que o produziu.

Cada tabela abre com um aviso de quatro linhas dizendo isso. Vale repetir aqui porque no Overleaf o
aviso e facil de ignorar: **um numero ajeitado a mao numa tabela e perdido na proxima
regeneracao**, e ate la deixa de corresponder a rodada. Para mudar um numero, muda-se a rodada ou o
gerador.

A prosa do `main.tex` e a bibliografia, essas sim, editam-se livremente aqui e no Overleaf.

## Regenerar

Do repositorio de pesquisa, com este repositorio ao lado:

```powershell
.venv\Scripts\python scripts\x3_paper_tables.py
.venv\Scripts\python scripts\x6_paper_figure.py
```

Os geradores escrevem direto aqui. Procuram, nesta ordem: a variavel `PDM2_PAPER_DIR`, a pasta irma
`handwriting-acquisition-floor-paper`, e por fim um `paper/` dentro do proprio repositorio de
pesquisa.

## Fluxo com o Overleaf

A sincronizacao e **manual**, nao continua: *Pull from GitHub* traz o que foi regenerado aqui,
*Push to GitHub* devolve o que foi editado la. Se os dois lados mexerem no mesmo arquivo, a
reconciliacao e na mao -- na pratica, convem regenerar e dar push **antes** de uma rodada de edicao
no Overleaf, nao durante.

## O que falta confirmar no texto

Os dois numeros de financiamento **ja estao preenchidos** nos dois documentos, trazidos do
camera-ready do VISAPP 2027 em 24/11/2026: o processo do PDSE (`88881.266133/2026-01`) e o projeto
do Angel (`PID2025-169751OB-I00`, Spanish State Research Agency). O que sobra e a **autoria deste
estudo**, cuja lista e ordem vieram daquele artigo e ainda precisa ser confirmada; esta marcada nos
dois arquivos com `[AUTHOR VERIFICATION REQUIRED]`.

No `main-mdpi.tex` restam outros quatro marcadores, todos de coisas que so os autores podem
afirmar: os papeis CRediT, a redacao de etica para analise secundaria de bases publicas, a rota de
acesso de cada coorte e os links de pre-registro que a revista exige. Ha ainda uma nota junto ao
financiamento: agencias espanholas costumam exigir formula propria de agradecimento, que pode
incluir o identificador `MICIU/AEI/10.13039/501100011033` --- vale conferir com a AEI.

## Como o artigo anterior e citado

O short paper do VISAPP 2027 entra em terceira pessoa, com a autoria real, o que o duplo-cego do
ICML permite para trabalho anterior. As duas passagens que o citam -- a seccao 1 e o paragrafo
"Reference cohort" da seccao 6 -- ja estavam escritas assim, de modo que nada muda no camera-ready.
A submissao em si continua anonima.

## Antes de tornar publico

`figures/examples.png` **esta versionado aqui**, ao contrario do que acontecia quando o artigo
morava dentro do repositorio de pesquisa: sem ele o documento nao compila no Overleaf. Mas a figura
traz tracos de gravacoes das bases, que nao sao nossas para redistribuir, e por isso este
repositorio fica privado. Numa eventual copia publica, a figura sai.

Enquanto o artigo nao estiver submetido, um repositorio publico com este titulo tambem identifica
os autores, o que importa se o destino tiver revisao cega.
