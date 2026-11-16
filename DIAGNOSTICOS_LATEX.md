# Diagnósticos LaTeX do TCC

Verificação realizada em 12/11/2026 no Windows, na instalação MiKTeX do projeto.

## Ambiente e reprodução

- Raiz: `documento.tex`; a linha 32 chama `\imprimirfolhaderosto{}`.
- Motor: pdfLaTeX, pdfTeX 1.40.28, MiKTeX 25.12.
- Formato: LaTeX2e 2025-11-01; camada L3 2025-12-24.
- Automatização: latexmk 4.88 (09/03/2026), BibTeX 0.99e, MakeIndex 2.16.
- Extensão instalada: LaTeX Workshop 10.20.0.
- Receita padrão: `TCC UFC (latexmk)`; reconstrução: `TCC UFC (compilacao limpa)`.
- Saída: `out/documento.pdf`. O comentário `% !TeX program = pdflatex` não substitui a receita: `latex-workshop.latex.build.enableMagicComments` está em `false`.

Comando da compilação limpa, a executar na pasta que contém `documento.tex`:

```powershell
latexmk -gg -pdf -interaction=nonstopmode -file-line-error -synctex=1 -outdir=out documento.tex
```

O parâmetro `-gg` limpa os produtos conhecidos da compilação antes de reconstruir. O latexmk executa o BibTeX com `abntex2-alf.bst` e repete o pdfLaTeX conforme as dependências. O TCC não imprime listas nem índice remissivo nesta versão, portanto não há etapa de listas a executar na compilação normal. A antiga inicialização de índice produzia um `.idx` vazio.

Para comparação, os arquivos versionados de `HEAD` (`2776377`) foram reconstruídos com `git show` em `tmp/latex-audit/baseline`, sem desfazer as correções locais. Essa cópia também foi compilada do zero. Foram lidos integralmente o log dessa cópia (1.602 linhas) e os logs finais; não se usou apenas a saída resumida do terminal. Os artefatos de investigação ficam em `tmp/latex-audit/`, ignorado pelo Git.

Não foi lida uma sessão ativa do painel Problems. A correspondência abaixo foi reconstruída a partir das mensagens fornecidas e do log original: **13 ocorrências de avisos LaTeX**, mais **um aviso adicional do pdfTeX**. A versão local já continha correções de cinco dessas ocorrências antes desta investigação. Mensagens que não reaparecem no log final são antigas em relação a esta compilação; a contagem do editor só pode ser confirmada depois de recompilar a raiz correta.

## Correspondência dos 13 diagnósticos

| Mensagem do log original | Ocorrências | Resultado final |
| --- | ---: | --- |
| `Unused global option(s): [section,subsection]` | 1 | Resolvida |
| `No \printglossary or \printglossaries found` | 1 | Resolvida |
| `Underfull \hbox (badness 10000)` na chamada da folha de rosto | 2 | Resolvidas |
| `Overfull \hbox (4.56003pt too wide)` na mesma chamada | 1 | Resolvida |
| `No 'datatool' support for dialect 'english'` | 1 | Não ocorre com o recurso sem uso desativado |
| Mesma mensagem para `spanish` | 1 | Não ocorre com o recurso sem uso desativado |
| Mesma mensagem para `brazil` | 2 | Não ocorre com o recurso sem uso desativado |
| `Overriding \printglossary` | 1 | Não ocorre com o recurso sem uso desativado |
| `Overriding 'theglossary' environment` | 1 | Não ocorre com o recurso sem uso desativado |
| Babel: `Name 'brazil' is deprecated` | 1 | Persiste; ver abaixo |
| memoir: `\settocpreprocessor is marked deprecated` | 1 | Persiste; ver abaixo |
| **Total** | **13** | **11 ocorrências resolvidas; 2 persistem** |

Além das 13 ocorrências, o pdfTeX emitia `destination with the same identifier (name{page.1}) has been already used, duplicate ignored`. A configuração `hypertexnames=false` mantém a numeração impressa e gera identificadores internos distintos. Esse aviso também foi eliminado.

Os avisos transitórios de citações e sumário ausentes nas primeiras passagens de uma compilação limpa desaparecem após o BibTeX e as passagens seguintes. Não são erros finais do TCC. As execuções finais terminaram com código 0 e `All targets (out/documento.pdf) are up-to-date`.

## Opções de seção e formatação

O arquivo original declarava `section=Title` e `subsection=Title` na classe. A classe instalada só declara `section=TITLE` e `subsection=TITLE`, sensíveis a maiúsculas; essas opções válidas transformam os títulos em caixa alta, não controlam a numeração.

As opções com `Title` não eram aceitas pela classe e seguiam como opções globais sem consumidor. Foram removidas. Não foram substituídas por `TITLE`, porque o projeto prevê seções em caixa de frase. `chapter=TITLE`, os comandos de títulos do modelo UFC e as configurações de numeração foram preservados. A comparação dos arquivos `.toc` confirmou os mesmos títulos, níveis e páginas, incluindo seções e subseções.

## Glossário, siglas, listas e idiomas

A busca abrangeu os capítulos incluídos, `lib/preambulo.tex`, `lib/ufctex.sty`, `1-pre-textuais/lista-de-abreviaturas-e-siglas.tex` e `3-pos-textuais/glossario.tex`.

- O arquivo de siglas contém apenas um comentário; o arquivo de glossário está vazio.
- Não há entradas `\newacronym` ou `\newglossaryentry`, nem usos de `\gls`, variantes ou impressão dessas listas nos capítulos atuais.
- O documento informa explicitamente que resumo, abstract e listas ainda dependem da versão final. Não se inventaram esses elementos nem se adicionaram páginas vazias.
- A lista de símbolos e os comandos de listas de figuras/tabelas do modelo não dependem da inicialização de glossário e foram preservados.

O pacote e sua inicialização agora são opcionais, controlados por `\UFCglossariosfalse`. As definições dependentes em `ufctex.sty` só são executadas se o pacote estiver carregado. O índice remissivo também não é inicializado sem uso. Isso elimina a dependência desnecessária, sem filtros de avisos nem substituições vazias de comandos de diagnóstico.

Foram preservados `english`, `spanish` e `brazil`. O texto atual está em português do Brasil; os outros idiomas vêm do modelo e não há resumos para justificar uma mudança nesta revisão. A remoção do pacote de glossário sem uso não muda a seleção de idioma do Babel nem a hifenização do texto.

### Origem dos avisos de tracklang/datatool

Versões identificadas no log original:

| Dependência | Versão |
| --- | --- |
| glossaries | 5.1, 21/04/2026 |
| tracklang | 1.6.8, 24/05/2026 |
| datatool-base | 3.4.4, 31/07/2026 |

`glossaries` carrega `datatool-base`, que pede a `tracklang` os arquivos de localização dos dialetos registrados. A chamada aparece na linha 9924 de `datatool-base.sty`. A instalação não forneceu suporte de localização datatool para os dialetos listados, embora o próprio glossaries tenha carregado seus dicionários English, Spanish e Brazilian. O log registra quatro ocorrências, com `brazil` repetido.

Isso não significa que o português ou os outros idiomas estejam sem suporte no Babel. A localização datatool é distinta da localização do glossaries; em particular, sua ausência não impede a impressão com `\printglossary` e MakeIndex. A mantenedora documenta essa distinção no [registro 300 do datatool](https://dickimaw-books.com/bugtracker.php?key=300) e no [manual do glossaries](https://mirror.las.iastate.edu/tex-archive/macros/latex/contrib/glossaries/glossaries-user.pdf).

Se o recurso for ativado futuramente, os avisos podem reaparecer. A ação específica para usar ordenação localizada interna do datatool é instalar os arquivos de idioma/região correspondentes disponibilizados para essa versão e verificar o suporte ao dialeto desejado. Para o fluxo testado com MakeIndex, a ausência não impediu a geração das listas. Não se usou `lang-warn=false`, downgrade de pacotes ou remoção de idiomas para esconder mensagens.

### Redefinições do glossaries e teste opcional

Não há carregamento duplicado do pacote no projeto. `memoir.cls` já define `\printglossary` e `theglossary`; `glossaries.sty` detecta essas definições e as substitui por sua implementação, emitindo as duas mensagens. Portanto, a origem é a coexistência das duas implementações, não dois `\usepackage{glossaries}`. Com o recurso inativo, não há substituição.

Também foram atualizadas macros opcionais antigas do modelo: `\glossarystyle` foi substituído por `\setglossarystyle`, o nome inexistente `glossario-uece` foi corrigido para o estilo definido `glossario-ufc`, e a formatação das entradas usa `\glossentry` da versão atual. A opção `acronym` registra o tipo específico usado pela lista de siglas.

Essas alterações foram verificadas numa cópia isolada em `tmp/latex-audit/glossary-probe`, com o recurso ativado, uma sigla e uma entrada de glossário artificiais. O MakeIndex aceitou uma entrada em cada lista, sem rejeições ou avisos; a compilação posterior terminou com código 0 e o texto extraído contém a sigla expandida e a definição do glossário. Nada desse conteúdo de teste foi incluído no TCC. A sequência para ativação futura é:

1. Alterar `\UFCglossariosfalse` para `\UFCglossariostrue` no preâmbulo.
2. Definir entradas e usá-las nos capítulos; incluir `\imprimirlistadeabreviaturasesiglas` no pré-textual e `\imprimirglossario` no local previsto para o glossário.
3. Após a primeira passagem, gerar os dois tipos de lista com MakeIndex:

```powershell
pdflatex -interaction=nonstopmode -halt-on-error -file-line-error -output-directory=out documento.tex
makeglossaries -d out documento
latexmk -pdf -interaction=nonstopmode -file-line-error -synctex=1 -outdir=out documento.tex
```

Atualmente essa etapa não integra a receita normal porque não há listas em uso. Se forem incorporadas ao TCC, a receita deve passar a executar `makeglossaries` após a primeira passagem e antes das passagens finais. O teste manteve os avisos das dependências ativos.

## Ajuste da folha de rosto

A linha 32 de `documento.tex` apenas expande a macro institucional; o problema real estava em `\folhaderostocontent`, em `lib/ufctex.sty`.

- O texto de apresentação terminava em `\\` e a macro acrescentava `\newline` e outra quebra após o orientador, produzindo linhas vazias justificadas e os dois avisos Underfull.
- O posicionamento somava indentação, deslocamentos fixos e espaços entre comandos ao bloco de 8 cm, causando o excesso de 4,56003 pt.
- O término do parágrafo agora é explícito com `\par`; o intervalo antes do orientador usa `\medskip`. O bloco de 8 cm é alinhado à direita por `\noindent\hfill` e encerrado com `\par`.

Foram preservados A4, margens de 3 cm/2 cm, fonte, tamanho, espaçamento simples do bloco e os afastamentos verticais principais. Não se elevaram `\hbadness` ou `\hfuzz`, nem se aplicou `\sloppy` globalmente. A folha de rosto foi renderizada e conferida; não há texto fora das margens.

## Dois avisos persistentes das dependências

### Babel e abntex2

```text
Package babel Warning: Name 'brazil' is deprecated.
(babel)                Use 'brazilian' instead.
(babel)                Reported on input line 4320.
```

- Versões: Babel 25.17 (11/12/2025) e abntex2 1.9.7 (24/11/2018).
- Origem: `abntex2.cls` carrega explicitamente `\RequirePackage[brazil]{babel}` na linha 138 e usa `\captionsbrazil`. O próprio projeto também declara o identificador compatível com a classe.
- Impacto observado: aviso de nome obsoleto; português do Brasil, títulos institucionais e hifenização continuam ativos. Não impede o PDF.
- Ação que resolve a origem: adotar uma versão da classe compatível com `brazilian`, atualizando também suas referências a `\captionsbrazil` e verificando as personalizações UFC. Mudar somente a opção da raiz não remove a exigência `brazil` dentro da classe. A atualização da classe deve ser feita como dependência revisada, com nova conferência visual, sem editar manualmente a instalação MiKTeX.

### memoir e abntex2

Mensagem completa do log:

```text
Class memoir Warning: \settocpreprocessor is marked deprecated and will be
(memoir)              removed in 2026, the problem it tried to solve
(memoir)              (see manual, section 9.2.3),
(memoir)              has been fixed in the kernel, and the feature is
(memoir)              no longer needed. on input line 483.
```

- Versões: memoir 3.8.4b (04/11/2025), abntex2 1.9.7 e kernel LaTeX 2025-11-01.
- Origem: a classe antiga chama `\settocpreprocessor` para transformar títulos do sumário; há também personalizações correspondentes no modelo UFC. A primeira emissão ocorre durante o carregamento de `abntex2.cls`, antes do preâmbulo do projeto.
- Impacto observado: aviso de migração, não erro. O comando ainda existe na versão testada; sumário, caixa dos títulos, links e numeração foram preservados.
- Ação que resolve a origem: migrar a classe e as personalizações UFC para o mecanismo atual de formatação de entradas `\cft...font`, conforme a seção 9.2.3 do [manual oficial do memoir](https://mirrors.mit.edu/CTAN/macros/latex/contrib/memoir/memman.pdf), e validar novamente caixa, apêndices e links. Remover só as chamadas no arquivo UFC não elimina a emissão anterior na classe. Não se redefiniu o comando para um corpo vazio nem se alterou `memoir.cls`.

## Resultado e preservação

- PDF final: 18 páginas A4, sem erros, citações indefinidas, referências pendentes, caixas Underfull/Overfull ou identificadores de página duplicados no log estabilizado.
- Conferência visual: capa, folha de rosto (a página afetada), sumário e bibliografia. Resumos e listas não existem na versão atual; não é possível validar páginas que o projeto não imprime.
- Texto extraído do PDF original e do corrigido é idêntico quando se normalizam espaços e quebras de linha. A diferença de quebra observada ficou restrita ao bloco ajustado da folha de rosto.
- Mesmos títulos, níveis e páginas no `.toc`, desconsiderando os identificadores internos dos links; capítulos 1 a 7 e subseções preservados. Bibliografia `.bbl` idêntica à original.
- Conteúdo dos capítulos e do `.bib` não foi alterado. Instalação MiKTeX e configurações de filtragem de diagnósticos não foram modificadas.

Arquivos alterados em relação ao `HEAD`: `documento.tex`, `lib/preambulo.tex`, `lib/ufctex.sty`, `.vscode/settings.json`, `LEIA-ME.md` e este relatório. Parte das correções nos três primeiros e na configuração da extensão já estava na árvore local antes desta investigação; foi preservada e revalidada.

## Cuidados com auxiliares antigos no editor e na pasta sincronizada

No VS Code, abra a pasta completa, selecione `documento.tex` e execute **LaTeX Workshop: Build with recipe → TCC UFC (compilacao limpa)**. A receita normal continua disponível para compilações incrementais. Confira a data de `out/documento.log` e visualize `out/documento.pdf`, não a cópia antiga da raiz. Se o painel ainda mostrar mensagens ausentes no novo log, recarregue a janela do VS Code e recompile a raiz; os filtros de diagnósticos permanecem ativos.

Durante a investigação também foram encontrados auxiliares renomeados (`documento 2.aux` até `documento 7.aux`, além de `.fls` duplicado). Uma tentativa incremental, com `.aux` ausente mas cache anterior existente, falhou no BibTeX por falta de `\citation`, `\bibdata` e `\bibstyle`. A compilação limpa reconstruiu esses arquivos e concluiu; uma compilação incremental posterior também terminou com código 0. A pasta está no iCloudDrive; os sufixos são compatíveis com conflitos de sincronização, embora a origem exata do processo externo não tenha sido rastreada. Se isso continuar, compile uma cópia/clonagem local fora da pasta sincronizada e use Git para sincronizar os fontes. Nenhum auxiliar duplicado foi tratado como fonte ou incluído no repositório.

As ferramentas Perl também informaram, neste terminal, que `LC_ALL=C.UTF-8` não é uma localidade suportada no Windows e usaram `Portuguese_Brazil.1252` como alternativa. Essa mensagem é do ambiente do processo, não do `.log` LaTeX nem das 13 ocorrências analisadas; não impediu as compilações concluídas.
