# E-16 — Normalização bibliográfica

Issue #18. Revisão parcial para aprovação do autor; não encerrar a issue antes da verificação final.

## Referenciais consultados em 17 nov. 2026

- [Sistema de Bibliotecas da UFC — normalização](https://biblioteca.ufc.br/pt/servicos-e-produtos/normalizacao-de-trabalhos-academicos/): guias institucionais.
- [Guia de citações UFC, 2025](https://biblioteca.ufc.br/wp-content/uploads/2025/06/guianormalizacaocitacoes2025.pdf), p. 10, exemplos de chamadas com nomes em caixa normal, conforme NBR 10520:2023.
- [Guia de referências UFC, 2023](https://biblioteca.ufc.br/wp-content/uploads/2023/12/guianormalizacaoreferencias.pdf): antecede a NBR 6023:2025.
- [Guia de trabalhos acadêmicos UFC, 2022](https://biblioteca.ufc.br/wp-content/uploads/2022/05/guianormalizacaotrabalhosacademicos-17.05.2022.pdf), p. 9: referência à edição 2011 da NBR 14724. A edição 2024 é posterior; confrontar com a orientação institucional atual.
- NBR 6023:2025, itens 6, 7.11, 8.1, 8.4 e 8.5: uniformidade, identificação dos atos, autoria, local e editora. Consultar a coleção de normas via biblioteca.
- [Templates UFC](https://biblioteca.ufc.br/pt/servicos-e-produtos/templates/): modelo Overleaf/LaTeX indicado como em atualização. Preservou-se o modelo ufctex entregue pelo aluno.
- [REN 1059](https://www2.aneel.gov.br/cedoc/ren20231059.pdf), [REN 1000 — republicação no DOU de 21 jan. 2022](https://pesquisa.in.gov.br/imprensa/servlet/INPDFViewer?captchafield=firstAccess&data=21%2F01%2F2022&jornal=515&pagina=74), [Lei 6496](https://www.planalto.gov.br/ccivil_03/leis/l6496.htm): ementas identificadas em fontes oficiais indexadas. Os acessos anteriores registrados no arquivo foram preservados quando a URL não mudou.

## Ajustes e justificativa técnica

- Registrada a autoria institucional da ANEEL por extenso, com sigla; 0126 identificada como documento da Enel Distribuição Ceará. Retirado o campo geográfico Ceará da publicação da 0126, pois área de concessão não comprova o local editorial. Mantidas as identificações das fontes particulares e a ausência dos dados que devem permanecer reservados.
- Ajustadas as ementas das REN 1000 e 1059 e da Lei 6496. Alterada a URL da REN 1059 para o endereço oficial indexado identificado nesta consulta.
- Mantido abntex2cite/BibTeX. A opção local ufc-citacao-2023 configura a saída autor-data em caixa normal por meio de entrada ABNT-options no arquivo .bib, acionada com citeoption após begin{document}. Não integra a lista de referências. O uso direto da opção AuthorYEAR do pacote testado causou colisão entre chaves em BibTeX, que não diferencia capitalização; por isso adotou-se uma chave distinta. Ajustado o limiar de abreviação de autores de 2 para 3, com lista bibliográfica completa preservada.
- Teste reduzido em TeX Live, abntex2-alf 1.9.7, pdflatex e BibTeX: a opção local produziu “(Silveira; Córdova, 2009)”, “Silveira e Córdova (2009)” e chamadas institucionais em caixa normal, sem erro de BibTeX. Não se trata de compilação do TCC completo nem de certificação ABNT.
- Conferência estática dos sete arquivos textuais: 19 chaves bibliográficas e 19 chaves citadas, nenhuma ausente ou não citada; quatro marcadores REVISAR preservados.

## Conferência local obrigatória antes do encerramento

1. Executar compilação limpa, usando a receita do LEIA-ME.md. Conferir documento.bbl, documento.blg, documento.log e PDF integral. Testar chamadas com dois autores, autores institucionais, documentos sem autoria divulgada e localizadores; observar possíveis quebras de linha de nomes institucionais extensos.
2. Verificar caixa alta das entradas institucionais na lista final, inclusive o tratamento de nomes protegidos por chaves e acentos no estilo legado; o teste reduzido mostrou que os autores institucionais podem permanecer em caixa normal na bibliografia. O ajuste das chamadas não resolve automaticamente a formatação das referências.
3. Conferir uniformidade tipográfica, alinhamento, espaçamento, pontuação, ementas e dados oficiais de publicação dos atos; local/editora quando aplicáveis, data do catálogo Enel sem data identificada, DOI/URL e datas de acesso. Não inventar local, editora ou data. Conferir a paginação exata da unidade de Silveira e Córdova: a página inicial do texto indexado é 33, embora a referência atual tenha 31–42; a abertura integral do PDF do repositório UFRGS não foi bem-sucedida nesta consulta. Manter o registro pendente até confirmar limites da unidade.
4. Reabrir os documentos históricos NT-003/2012, NT-002/2011, NT-C 003/2016, a NBR 5410 e o livro e capítulo para revisão integral de metadados; nesta etapa não foram todos revalidados. Verificar com a Biblioteca a entrada por título e os créditos das fontes particulares, conforme a E-13. A autorização de divulgação permanece pendente.
5. Confirmar requisitos atualizados NBR 14724:2024 e 6023:2025 com orientador/Biblioteca UFC, incluindo os pré-textuais finais e a lista de símbolos (E-22). Repetir conferência após completar os capítulos pendentes e acrescentar novas referências.

O ajuste foi deliberadamente conservador para não substituir a configuração de compilação anteriormente validada no Windows por outro sistema sem validação. Não há declaração de conformidade integral nem encerramento antecipado da issue #18.
