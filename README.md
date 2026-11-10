# prompts-ia

Biblioteca de prompts para tarefas de suporte operacional, com versões testadas e registro das iterações.

> **Status:** em construção (prompt 01 testado até a v2). Todos os chamados usados nos testes são **fictícios**. Nenhum dado real de pessoas ou instituições foi usado.

## Problema

Times de suporte repetem as mesmas tarefas de texto o dia todo: entender o chamado, classificar, responder, escalar. Sem prompts documentados, o resultado de uma IA varia de pessoa para pessoa e de dia para dia.

## Solução

Sete prompts para tarefas reais de suporte. Cada um tem objetivo, entrada, saída esperada, exemplo e o histórico do que mudou da v1 até a v3, com base em testes no mesmo conjunto de chamados fictícios.

## Os prompts

| # | Prompt | Status |
|---|---|---|
| 01 | [Classificar chamado](prompts/01-classificar-chamado.md) | v1 e v2 testadas; v3 pendente |
| 02 | Resposta inicial ao solicitante | a fazer |
| 03 | Resumir um problema | a fazer |
| 04 | Escrever procedimento | a fazer |
| 05 | Pedir informações que faltam | a fazer |
| 06 | Nota de escalonamento N1 para N2 | a fazer |
| 07 | Resumo semanal de chamados | a fazer |

## Como foi testado

Todos os prompts rodam sobre os mesmos 6 chamados fictícios, descritos em [`testes/chamados-ficticios.md`](testes/chamados-ficticios.md). Cada chamado tem um comportamento esperado que vale para qualquer prompt (por exemplo, não inventar informação) e, para o prompt 02, uma descrição da resposta ideal. A cada versão, o resultado é comparado com isso e os erros são anotados na ficha do prompt, em `prompts/`. As saídas brutas ficam em [`testes/resultados/`](testes/resultados/).

## Resultados

Chamados em que o resultado atendeu ao comportamento esperado (cada chamado testado uma vez por versão):

| Prompt | v1 | v2 | v3 |
|---|---|---|---|
| 01 Classificar chamado | 2 de 6 (4 parciais) | 5 de 6 (1 parcial) | não testada |

**O que aprendi no prompt 01:** na v1, ao obrigar a IA a escolher sempre uma prioridade, ela chutava quando faltava informação ou quando o chamado não era técnico. Na v2, ao permitir os valores "indefinida" e "fora do escopo", esses casos (T02, T05, T06) passaram. O chamado com informação contraditória (T04) continuou parcial.

Modelo e data dos testes: **[preencher: nome do modelo e data]**.

## Limitações

- Cada chamado foi testado uma vez por versão; a estabilidade entre execuções não foi medida.
- 6 chamados fictícios e um único modelo: os números acima não permitem generalizar uma taxa de acerto.
- Não há usuários reais nem uso em produção.

## Melhorias futuras

- Ajustar o prompt 01 para apontar contradições (T04) e produzir JSON válido sem texto extra.
- Concluir os prompts 02 a 07.
- Usar o prompt 01 no Projeto 1 (triagem automática com n8n) e medir tempo e acerto em condições controladas.
