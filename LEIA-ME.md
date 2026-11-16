# TCC UFC — revisão dos capítulos 2 e 3

**Origem do modelo:** este projeto utiliza os arquivos do `Tcc.zip` fornecido pelo aluno, incluindo `lib/ufctex.sty` e `lib/logo-ufc.PNG`. O arquivo principal foi personalizado para o TCC de Engenharia Elétrica na UFC, Campus de Sobral.

## Compilação no VS Code (MiKTeX + Strawberry Perl)

Abra a raiz deste repositório no VS Code, abra `documento.tex` e use `Ctrl+Alt+B` com LaTeX Workshop. A receita do projeto executa LaTeX e BibTeX por meio do `latexmk`. No terminal, a partir da raiz, execute o mesmo fluxo:

```powershell
latexmk -cd -pdf -interaction=nonstopmode -halt-on-error -file-line-error -synctex=1 -outdir=. documento.tex
```

O PDF atualizado é gerado em `documento.pdf`, na raiz, junto aos arquivos auxiliares ignorados pelo Git. O argumento `-cd` fixa o diretório de trabalho no diretório do documento principal, e `-outdir=.` evita executar o BibTeX em uma pasta diferente da raiz, na qual o caminho relativo `3-pos-textuais/referencias.bib` poderia não ser encontrado. Não utilize a antiga receita com `-outdir=out` para este projeto. No MiKTeX Console, habilite a instalação automática de pacotes ausentes, caso necessário.

### Verificação de uma compilação limpa

Feche a visualização do PDF anterior, se necessário. Na raiz do projeto, execute:

```powershell
latexmk -cd -C -bibtex -outdir=. documento.tex
Remove-Item -Path documento.bbl -ErrorAction SilentlyContinue
latexmk -cd -pdf -interaction=nonstopmode -halt-on-error -file-line-error -synctex=1 -outdir=. documento.tex
```

Confirme que a compilação terminou sem erros, que `documento.bbl` foi gerado e que `documento.pdf` possui a seção REFERÊNCIAS e as citações resolvidas (sem `??`). Consulte `documento.log` e `documento.blg` se houver aviso persistente de referência/citação indefinida ou falha do BibTeX. Um PDF antigo em `out/documento.pdf` não será atualizado por este novo fluxo; utilize apenas o PDF da raiz. Os arquivos de compilação não devem ser adicionados ao Git.

A etapa E-01 foi testada em TeX Live (Linux); a validação do mesmo fluxo no MiKTeX/Windows deve ser realizada antes de encerrar a issue. A normalização bibliográfica de acordo com as normas ABNT e UFC é tratada separadamente na E-16.

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
