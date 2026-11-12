# prompts-ia

Biblioteca de prompts para tarefas de suporte operacional, com versões testadas e registro das iterações.

> **Status:** em construção. Prompts 01 e 02 testados até a v2, prompt 03 até a v3, prompt 04 em preparação. Todos os chamados usados nos testes são **fictícios**. Nenhum dado real de pessoas ou instituições foi usado.

## Problema

Times de suporte repetem as mesmas tarefas de texto o dia todo: entender o chamado, classificar, responder, escalar. Sem prompts documentados, o resultado de uma IA varia de pessoa para pessoa e de dia para dia.

## Solução

Sete prompts para tarefas reais de suporte. Cada um tem objetivo, entrada, saída esperada, exemplo e o histórico do que mudou da v1 até a v3, com base em testes em conjuntos fixos de casos fictícios.

## Os prompts

| # | Prompt | Status |
|---|---|---|
| 01 | [Classificar chamado](prompts/01-classificar-chamado/) | v1 e v2 testadas; v3 pendente |
| 02 | [Resposta inicial ao solicitante](prompts/02-resposta-inicial/) | v1 e v2 testadas; v3 pendente |
| 03 | [Resumir um problema](prompts/03-resumir-problema/) | v1, v2 e v3 testadas |
| 04 | [Escrever procedimento](prompts/04-escrever-procedimento/) | v1 a testar |
| 05 | [Pedir informações que faltam](prompts/05-pedir-informacoes/) | a fazer |
| 06 | [Nota de escalonamento N1 para N2](prompts/06-nota-escalonamento/) | a fazer |
| 07 | [Resumo semanal de chamados](prompts/07-resumo-semanal/) | a fazer |

## Estrutura do repositório

```
prompts/
  NN-nome-do-prompt/
    README.md        ficha do prompt: objetivo, prompt atual, versões e resultados
    resultados/      saídas brutas de cada versão (v1.md, v2.md, ...)
testes/              conjuntos de casos fictícios usados nos testes
docs/                modelo de ficha
```

## Como foi testado

Cada prompt é testado em um conjunto fixo de 6 casos fictícios, sempre os mesmos em todas as versões, para poder comparar:

- prompts 01, 02 e 05: [`testes/chamados-ficticios.md`](testes/chamados-ficticios.md);
- prompts 03 e 06 (trabalham com conversas): [`testes/conversas-ficticias.md`](testes/conversas-ficticias.md);
- prompt 04 (transforma anotações em procedimento): [`testes/solucoes-ficticias.md`](testes/solucoes-ficticias.md).

Cada caso tem um comportamento esperado (por exemplo, não inventar informação). A cada versão, o resultado é comparado com isso e os erros são anotados na ficha do prompt. As saídas brutas ficam na pasta `resultados/` de cada prompt.

## Resultados

Casos em que o resultado atendeu ao comportamento esperado (cada caso testado uma vez por versão):

| Prompt | v1 | v2 | v3 |
|---|---|---|---|
| 01 Classificar chamado | 2 de 6 (4 parciais) | 5 de 6 (1 parcial) | não testada |
| 02 Resposta inicial | 3 de 6 (3 parciais) | 5 de 6 (1 parcial) | não testada |
| 03 Resumir um problema | 5 de 6 (1 parcial) | 6 de 6 | 5 de 6 (1 parcial) |

**O que aprendi no prompt 01:** na v1, ao obrigar a IA a escolher sempre uma prioridade, ela chutava quando faltava informação ou quando o chamado não era técnico. Na v2, ao permitir os valores "indefinida" e "fora do escopo", esses casos (T02, T05, T06) passaram. O chamado com informação contraditória (T04) continuou parcial.

**O que aprendi no prompt 02:** na v1, a IA usava sempre o mesmo molde de resposta, nunca admitia que não sabia e não dizia quando escalar. Na v2, regras explícitas de honestidade e de urgência corrigiram T02, T03 e T06 (e as ressalvas de T01 e T05). O chamado com contradição (T04) continuou parcial. Como a v2 mudou várias regras de uma vez, não é possível atribuir cada melhoria a uma regra específica.

**O que aprendi no prompt 03:** uma instrução simples já resumiu bem 5 das 6 conversas; a falha (C4) foi ir além da conversa, concluindo que o repasse estava "atrasado" e recomendando ações. Uma única regra de fidelidade ("só fatos explícitos") corrigiu isso (v2, 6 de 6), mas fez sumir o status do chamado. A v3 trouxe formato fixo com status explícito, o que o Projeto 1 precisa, mas a lista fechada de status forçou uma escolha ruim em C2 ("Aguardando informação" onde "Não resolvido" seria melhor). A v3 foi adotada pelo formato; o erro de status ficou registrado como limitação.

Padrão que se repetiu nos três prompts: quando o prompt obriga a IA a escolher (prioridade, status, estrutura), ela escolhe mesmo sem uma opção boa; dar uma saída honesta ("indefinida", "fora do escopo", "não sei") melhora o resultado.

Modelo e data dos testes: **[preencher: nome do modelo e data]**.

## Limitações

- Cada caso foi testado uma vez por versão; a estabilidade entre execuções não foi medida.
- 6 casos fictícios por conjunto e um único modelo: os números acima não permitem generalizar uma taxa de acerto. No prompt 03 a v1 já passou em 5 de 6, então o conjunto provavelmente é fácil.
- A avaliação de cada resposta é do próprio autor, comparando com o comportamento esperado de cada caso; não há usuários reais nem uso em produção.

## Melhorias futuras

- Prompts 01 e 02: apontar contradições do relato (T04); no 01, produzir também JSON válido sem texto extra.
- Prompt 03: esclarecer quando usar "Aguardando informação" e quando usar "Não resolvido".
- Concluir os prompts 04 a 07.
- Usar o prompt 01 no Projeto 1 (triagem automática com n8n) e medir tempo e acerto em condições controladas.
