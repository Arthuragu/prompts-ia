# prompts-ia

Biblioteca de prompts para tarefas de suporte operacional, com versões testadas e registro das iterações.

> **Status:** em construção (prompts 01 e 02 testados até a v2). Todos os chamados usados nos testes são **fictícios**. Nenhum dado real de pessoas ou instituições foi usado.

## Problema

Times de suporte repetem as mesmas tarefas de texto o dia todo: entender o chamado, classificar, responder, escalar. Sem prompts documentados, o resultado de uma IA varia de pessoa para pessoa e de dia para dia.

## Solução

Sete prompts para tarefas reais de suporte. Cada um tem objetivo, entrada, saída esperada, exemplo e o histórico do que mudou da v1 até a v3, com base em testes no mesmo conjunto de chamados fictícios.

## Os prompts

| # | Prompt | Status |
|---|---|---|
| 01 | [Classificar chamado](prompts/01-classificar-chamado.md) | v1 e v2 testadas; v3 pendente |
| 02 | [Resposta inicial ao solicitante](prompts/02-resposta-inicial.md) | v1 e v2 testadas; v3 pendente |
| 03 | [Resumir um problema](prompts/03-resumir-problema.md) | v1 a testar |
| 04 | Escrever procedimento | a fazer |
| 05 | Pedir informações que faltam | a fazer |
| 06 | Nota de escalonamento N1 para N2 | a fazer |
| 07 | Resumo semanal de chamados | a fazer |

## Como foi testado

Todos os prompts rodam sobre os mesmos 6 chamados fictícios, descritos em [`testes/chamados-ficticios.md`](testes/chamados-ficticios.md). Cada chamado tem um comportamento esperado que vale para qualquer prompt (por exemplo, não inventar informação) e, para o prompt 02, uma descrição da resposta ideal. A cada versão, o resultado é comparado com isso e os erros são anotados na ficha do prompt, em `prompts/`. Os prompts que trabalham com conversas (03 e 06) usam outro conjunto, de 6 conversas fictícias, em [`testes/conversas-ficticias.md`](testes/conversas-ficticias.md). As saídas brutas ficam em [`testes/resultados/`](testes/resultados/).

## Resultados

Chamados em que o resultado atendeu ao comportamento esperado (cada chamado testado uma vez por versão):

| Prompt | v1 | v2 | v3 |
|---|---|---|---|
| 01 Classificar chamado | 2 de 6 (4 parciais) | 5 de 6 (1 parcial) | não testada |
| 02 Resposta inicial | 3 de 6 (3 parciais) | 5 de 6 (1 parcial) | não testada |

**O que aprendi no prompt 01:** na v1, ao obrigar a IA a escolher sempre uma prioridade, ela chutava quando faltava informação ou quando o chamado não era técnico. Na v2, ao permitir os valores "indefinida" e "fora do escopo", esses casos (T02, T05, T06) passaram. O chamado com informação contraditória (T04) continuou parcial.

**O que aprendi no prompt 02:** na v1, a IA usava sempre o mesmo molde de resposta, nunca admitia que não sabia e não dizia quando escalar. Na v2, regras explícitas de honestidade e de urgência corrigiram T02, T03 e T06 (e as ressalvas de T01 e T05). O chamado com contradição (T04) continuou parcial. Como a v2 mudou várias regras de uma vez, não é possível atribuir cada melhoria a uma regra específica.

Modelo e data dos testes: **[preencher: nome do modelo e data]**.

## Limitações

- Cada chamado foi testado uma vez por versão; a estabilidade entre execuções não foi medida.
- 6 chamados fictícios e um único modelo: os números acima não permitem generalizar uma taxa de acerto.
- A avaliação de cada resposta é do próprio autor, comparando com o critério de cada chamado; não há usuários reais nem uso em produção.

## Melhorias futuras

- Ajustar os prompts 01 e 02 para apontar contradições (T04); no 01, produzir também JSON válido sem texto extra.
- Concluir os prompts 03 a 07.
- Usar o prompt 01 no Projeto 1 (triagem automática com n8n) e medir tempo e acerto em condições controladas.
