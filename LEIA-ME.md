# TCC UFC — revisão dos capítulos 2 e 3

**Origem do modelo:** este projeto utiliza os arquivos do `Tcc.zip` fornecido pelo aluno, incluindo `lib/ufctex.sty` e `lib/logo-ufc.PNG`. O arquivo principal foi personalizado para o TCC de Engenharia Elétrica na UFC, Campus de Sobral.

## Compilação no VS Code (MiKTeX + Strawberry Perl)

Abra esta pasta no VS Code, abra `documento.tex` e use `Ctrl+Alt+B` com LaTeX Workshop. No terminal, pode executar:

```powershell
latexmk -pdf -interaction=nonstopmode -file-line-error -outdir=out documento.tex
```

O PDF é gerado em `out/documento.pdf`. No MiKTeX Console, habilite a instalação automática de pacotes ausentes, caso necessário.

## Alterações feitas conforme as correções do orientador

- Texto dos capítulos 2 e 3 reescrito em estilo técnico-acadêmico, sem tom de conversa nem passagens que se dirigem ao leitor.
- Hierarquia de títulos delegada ao modelo UFC, com títulos de seções grafados em caixa de frase.
- Denominação uniforme: códigos completos na primeira referência e «especificação 0126» / «especificação 1580» nas demais.
- Termo «recorte» substituído por «delimitação» ou «área de aplicação».
- Edifício Palatium apresentado como empreendimento residencial localizado em Sobral, sem identificadores privados desnecessários.
- Documento do projeto descrito como «memorial de cálculo elétrico, revisão 04».
- Metodologia concentrada nos procedimentos de pesquisa, sem descrever a organização dos capítulos.
- Citações associadas ao arquivo `.bib`, não lançadas apenas como texto livre.
- Não foi desenvolvido o Capítulo 4.

## Limitações de normalização

O modelo `ufctex` fornecido possui últimas alterações documentadas em 2019 e carrega `abntex2cite`, que antecede a ABNT NBR 10520:2023. Neste rascunho as citações no texto foram preferencialmente integradas à oração (`\citeonline`), mas **as referências devem ser verificadas na revisão final**, inclusive quanto a capitalização e demais alterações da ABNT NBR 6023:2025.

A Biblioteca da UFC informa que seu modelo LaTeX está em atualização. Consulte os guias oficiais de normalização da UFC e, antes da entrega definitiva, submeta o PDF à revisão de normalização bibliográfica.

O PDF foi preparado como entrega de **capítulos parciais**. A numeração inicia em 2 por `\setcounter{chapter}{1}`; quando for adicionada a Introdução, remova esse comando e inclua o capítulo 1. Elementos pré-textuais ainda não finalizados (resumos, folha de aprovação e ficha catalográfica) foram intencionalmente omitidos nesta versão para evitar dados fictícios.

A aprovação do projeto Palatium está documentada, mas a carta não enumera os dispositivos normativos efetivamente empregados pela concessionária. A hipótese de comparação com o referencial anterior é mantida sem extrapolar o teor da carta.
