# Matriz comparativa — instrumento de registro (E-14)

Os dois CSV constituem um único instrumento relacional de registro da comparação normativa e dos impactos técnicos. Os registros inseridos correspondem a análises de requisitos efetivamente examinados; o levantamento é progressivo. Utilizar UTF-8 e delimitador ponto e vírgula. No Excel, importar por Dados > De Texto/CSV, mantendo códigos e localizadores como texto. Preservar cabeçalhos, usar aspas duplas para conteúdo com ponto e vírgula, aspas ou quebra de linha, e exportar novamente em UTF-8 com o mesmo delimitador.

## Registro principal: matriz-comparativa.csv

Uma linha por requisito técnico ou documental comparado, ou por exclusão/dúvida territorial identificada. Desdobrar prescrições independentes, sem duplicar uma mesma classificação. Atribuir código único e estável (por exemplo, RN-0001: exemplo de formato, não registro real). Não renumerar ao ordenar por tema.

| Campo | Preenchimento |
|---|---|
| id_requisito | Código único e permanente. |
| tema | Tema técnico da seção 5.3. |
| dispositivo_0126 / dispositivo_1580 | Localizadores exatos do documento/versão, seção, item, alínea, nota, tabela, desenho, anexo e página quando necessária. Em caso de ausência, indicar que não foi identificado correspondente e os trechos consultados; não inventar item. |
| requisito_0126 / requisito_1580 | Descrição fiel da prescrição e suas condições de aplicação; registrar ausência ou impossibilidade de descrição, quando pertinente. |
| categoria_normativa | Mantido; Alterado; Acrescentado; Retirado; Reorganizado; Inconclusivo — exatamente uma categoria para cada requisito comparado. Exclusão territorial ou aplicabilidade não determinada: deixar sem categoria caso a comparação não tenha sido realizada, com justificativa. |
| aplicabilidade_ceara | Sim; Não; Não determinada. Separar exclusões e dúvidas da base de requisitos aplicáveis, inclusive nas contagens. |
| justificativa_normativa_ou_exclusao | Explicação da categoria, condição regional e motivo de exclusão ou dúvida. Distinguir interpretação de evidência. Quando demonstrada origem regulatória anterior, identificar ato, dispositivo e relação com o requisito em cada versão. Não criar categoria adicional nem tratar a origem regulatória como prova de manutenção ou novidade documental. |
| selecao_palatium | Sim; Não; Não determinada. Sim somente quando os três critérios da seção 5.4 forem atendidos. |
| justificativa_selecao | Demonstrar aplicabilidade ao Ceará, mudança técnica/documental e correspondência documental, ou indicar a razão da não seleção/limitação. Preservar as diferenças sem efeito no caso. |
| ids_impactos_palatium | Códigos dos impactos vinculados, separados por vírgula; deixar vazio para requisitos não selecionados. |
| evidencias_normativas | Identificação das passagens, desenhos ou tabelas examinados que sustentam a comparação; verificar equivalentes em outras partes e remissões identificáveis. |
| hipoteses_incertezas | Hipóteses explícitas, documentação ausente, limites da interpretação ou dúvidas remanescentes. Se nenhuma identificada, registrar isso apenas após conferência. |
| estado_conferencia | Pendente de conferência; Em revisão; Conferido. |
| registro_conferencia | Datas, critérios verificados, divergências, valores/classificações anteriores e novos, justificativa das correções e, se houver, revisão externa efetivamente realizada. |

## Registro associado: impactos-palatium.csv

Uma linha por consequência técnica de um requisito selecionado, com código próprio (por exemplo, IP-0001) e id_requisito existente no registro principal. Um requisito pode ter mais de uma consequência, sem repetir sua classificação normativa. Não criar impactos para requisitos não selecionados.

| Campo | Preenchimento |
|---|---|
| id_impacto / id_requisito | Código único da consequência e código do requisito de origem. |
| solucao_documentada | Solução ou característica do projeto original efetivamente identificada. |
| evidencias_projeto | Documento, página, prancha, detalhe, quadro, cálculo ou outro localizador verificável; respeitar as decisões de divulgação documental. |
| consequencia_tecnica | Efeito demonstrável ou condicionado à aplicação da 1580; sem presumir obrigação retroativa de adequação. |
| categoria_impacto | Solução compatível; Adequação potencialmente necessária; Situação condicionada à avaliação da distribuidora; Informação documental insuficiente. Usar uma categoria por consequência. |
| justificativa_impacto | Relação entre a mudança, a evidência do projeto e a consequência; explicar a condição de avaliação quando pertinente. |
| hipoteses_incertezas | Parâmetros, hipóteses e condições, fontes de cálculo e dados faltantes. |
| estado_conferencia / registro_conferencia | Mesmas regras de conferência do registro principal, aplicadas à consequência. |

## Preenchimento e controle

1. Levantar e confrontar os requisitos da 0126 e da 1580. Registrar localizadores, descrição, evidência, interpretação e aplicabilidade territorial. Não inferir supressão de ausência isolada.
2. Aplicar as seis categorias da E-04 e os três critérios cumulativos da E-05. Dúvidas de seleção não são categorias de impacto. Não confundir comparação inconclusiva com informação documental insuficiente do caso.
3. Registrar separadamente cada consequência selecionada e seus localizadores, hipóteses e categoria E-05.
4. Realizar segunda passagem pelo pesquisador com retorno às fontes originais. Registrar divergências, correções e motivos. "Conferido" não equivale a "sem incertezas". Não declarar revisão independente sem ocorrência efetiva.
5. Antes da síntese, verificar códigos únicos, vínculos entre os CSV, classificação única por requisito, seleção cumulativa, registros de impacto somente para requisitos selecionados, justificativas e estados de conferência. Separar requisitos excluídos e de aplicabilidade incerta das contagens de requisitos aplicáveis.
6. Apresentar os principais achados no Capítulo 6, com os códigos de rastreio. Ao concluir a análise, apresentar integralmente os requisitos comparados e os impactos associados em quadros vinculados pelo código do requisito no Apêndice A, preservando as evidências, justificativas, hipóteses, incertezas e a legibilidade conforme o modelo UFC. Os campos estado_conferencia e registro_conferencia são controles internos de pesquisa: não compõem o quadro acadêmico nem precisam ser reproduzidos no apêndice. A matriz é apresentada em dois conjuntos vinculados para evitar um quadro excessivamente largo. Não inserir registros fictícios para preencher o apêndice, nem declarar o levantamento concluído enquanto ainda estiver em execução.

A existência de registros no instrumento não significa que a comparação integral ou a avaliação de todos os impactos já foi concluída. O Apêndice A será incorporado ao documento principal após a consolidação dos registros e a conferência prevista no procedimento.
