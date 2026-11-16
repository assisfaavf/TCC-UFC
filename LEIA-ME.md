# TCC UFC — revisão dos capítulos 2 e 3

**Origem do modelo:** este projeto utiliza os arquivos do `Tcc.zip` fornecido pelo aluno, incluindo `lib/ufctex.sty` e `lib/logo-ufc.PNG`. O arquivo principal foi personalizado para o TCC de Engenharia Elétrica na UFC, Campus de Sobral.

## Compilação no VS Code (MiKTeX + Strawberry Perl)

Abra a raiz deste repositório no VS Code, abra `documento.tex` e use `Ctrl+Alt+B` com LaTeX Workshop. A receita do projeto executa LaTeX e BibTeX por meio do `latexmk`. No terminal, a partir da raiz, execute o mesmo fluxo:

```powershell
latexmk -cd -pdf -interaction=nonstopmode -halt-on-error -file-line-error -synctex=1 -outdir=out documento.tex
```

O PDF atualizado e os arquivos auxiliares são gerados em `out/`, ignorado pelo Git. O argumento `-cd` fixa o diretório de trabalho no diretório do documento principal. O `latexmk` configura os caminhos de busca do BibTeX para encontrar `3-pos-textuais/referencias.bib`, mesmo com a saída em `out/`. A configuração do projeto desativa comentários de seleção do motor para garantir o uso da receita completa, com BibTeX e as passagens necessárias. No MiKTeX Console, habilite a instalação automática de pacotes ausentes, caso necessário.

### Verificação de uma compilação limpa

Feche a visualização do PDF anterior, se necessário. Na raiz do projeto, execute:

```powershell
latexmk -cd -gg -pdf -interaction=nonstopmode -halt-on-error -file-line-error -synctex=1 -outdir=out documento.tex
```

No VS Code, o mesmo comando está disponível em **LaTeX Workshop: Build with recipe → TCC UFC (compilacao limpa)**. Confirme que a compilação terminou sem erros, que `out/documento.bbl` foi gerado e que `out/documento.pdf` possui a seção REFERÊNCIAS e as citações resolvidas (sem `??`). Consulte `out/documento.log` e `out/documento.blg` se houver aviso persistente de referência/citação indefinida ou falha do BibTeX. Feche a visualização antiga de `documento.pdf` na raiz e use apenas `out/documento.pdf`. Os arquivos de compilação não devem ser adicionados ao Git.

O fluxo com saída em `out/` foi validado no Windows com MiKTeX 25.12 e latexmk 4.88. A normalização bibliográfica de acordo com as normas ABNT e UFC é tratada separadamente na E-16.

Nesta versão não há listas de siglas, glossário ou índice remissivo em uso. O recurso opcional de glossário está desativado por `\UFCglossariosfalse` em `lib/preambulo.tex`.

Consulte [DIAGNOSTICOS_LATEX.md](DIAGNOSTICOS_LATEX.md) para a reprodução dos 13 avisos, as versões testadas, a validação visual e os dois avisos remanescentes das dependências.

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
