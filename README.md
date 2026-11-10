# prompts-ia

Biblioteca de prompts para tarefas de suporte operacional, com versões testadas e registro das iterações.

> **Status:** em construção. Todos os chamados usados nos testes são **fictícios**. Nenhum dado real de pessoas ou instituições foi usado.

## Problema

Times de suporte repetem as mesmas tarefas de texto o dia todo: entender o chamado, classificar, responder, escalar. Sem prompts documentados, o resultado de uma IA varia de pessoa para pessoa e de dia para dia.

## Solução

Sete prompts para tarefas reais de suporte. Cada um tem objetivo, entrada, saída esperada, exemplo e o histórico do que mudou da v1 até a v3, com base em testes no mesmo conjunto de chamados fictícios.

## Os prompts

| # | Prompt | Status |
|---|---|---|
| 01 | Classificar chamado | a fazer |
| 02 | Resposta inicial ao solicitante | a fazer |
| 03 | Resumir um problema | a fazer |
| 04 | Escrever procedimento | a fazer |
| 05 | Pedir informações que faltam | a fazer |
| 06 | Nota de escalonamento N1 para N2 | a fazer |
| 07 | Resumo semanal de chamados | a fazer |

Os prompts ficam em [`prompts/`](prompts/). O conjunto de teste fica em [`testes/chamados-ficticios.md`](testes/chamados-ficticios.md).

## Como foi testado

Todos os prompts rodam sobre os mesmos 6 chamados fictícios. A cada versão, os resultados são comparados com a saída esperada e os erros são anotados na própria ficha do prompt.

## Resultados

A preencher após os testes. Só entram aqui observações que realmente aconteceram.

## Limitações

A preencher.

## Melhorias futuras

A preencher.
