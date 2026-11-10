# 01. Classificar chamado

## Objetivo
Classificar um chamado em categoria e prioridade para alimentar a triagem automática (Projeto 1).

## Entrada
Texto livre do chamado, como escrito pelo solicitante.

## Saída esperada
JSON com os campos `categoria`, `prioridade` e `justificativa` curta. Chamado vago ou fora do escopo deve ser marcado como tal, sem inventar categoria.

## Prompt (versão atual)
Versão atual: **v2**.

```
Responda em JSON com os campos: **categoria, prioridade e justificativa** chamado.

A prioridade deve ser classificada como "baixa", "média" ou "alta". Caso faltem informações suficientes para classificar o chamado, utilize "indefinida" e explique o motivo na justificativa.

Se o chamado estiver fora do escopo de suporte técnico, classifique a categoria como "fora do escopo" e explique o motivo na justificativa, sem tentar inventar uma classificação técnica.

Não invente informações. Quando não houver dados suficientes para identificar o problema, informe essa limitação.

Mantenha o JSON válido, organizado e sem comentários fora da estrutura.

chamado:
```

## Exemplo de uso
**Entrada (T03):** "URGENTE! A impressora de pedidos da loja Pastelaria Central (fictícia) está offline e é horário de almoço. Pedidos estão chegando e não saem impressos, já perdemos pelo menos 5 pedidos."

**Saída obtida (v2):**
```json
{
"categoria": "impressora",
"prioridade": "alta",
"justificativa": "A impressora de pedidos está offline durante o horário de almoço, impedindo a impressão dos pedidos e causando impacto direto na operação da loja. Pelo menos 5 pedidos já foram perdidos, caracterizando uma situação crítica que exige atendimento imediato."
}
```

## Histórico de versões

### v1
**Prompt:**
```
Classifique o chamado abaixo.
Responda em JSON com: categoria, prioridade (baixa, média, alta) e justificativa.

CHAMADO:
```

**O que testei:** os 6 chamados do conjunto de teste. Saída completa em [`testes/resultados/prompt-01-v1.md`](../testes/resultados/prompt-01-v1.md). Pela saída (lista única com `id`), os 6 foram processados juntos numa mesma conversa.

| Chamado | Resultado | Observação |
|---|---|---|
| T01 | passou | Conectividade do tablet; prioridade "média" é discutível, mas aceitável |
| T02 | parcial | Reconheceu a falta de informação, mas atribuiu prioridade "baixa" |
| T03 | passou | Prioridade alta, impacto operacional reconhecido |
| T04 | parcial | Viu os dois fatos, mas não apontou a contradição nem pediu esclarecimento; prioridade "média" sem base |
| T05 | parcial | Categoria "Financeiro", mas o prompt não oferece como marcar "fora do escopo"; prioridade "baixa" atribuída |
| T06 | parcial | Atribuiu prioridade "média" e não disse que não consegue confirmar o código |

**Resultado:** 2 passaram, 4 parciais, 0 falharam por completo.

**O que saiu errado:** o prompt obriga a IA a escolher sempre uma prioridade (baixa, média ou alta). Quando falta informação (T02, T06) ou o chamado não é técnico (T05), ela escolhe um valor mesmo sem base.

### v2
**O que mudei e por quê:** dei à IA uma saída para quando falta informação (valor "indefinida") e outra para chamados não técnicos ("fora do escopo"), porque o erro da v1 era ser forçada a chutar.

**Prompt:** ver "Prompt (versão atual)" acima.

**O que testei:** os mesmos 6 chamados, um por vez. Saída completa em [`testes/resultados/prompt-01-v2.md`](../testes/resultados/prompt-01-v2.md).

| Chamado | Resultado | Observação |
|---|---|---|
| T01 | passou | Prioridade "média", com ressalva de que falta informação sobre a extensão |
| T02 | passou | Categoria e prioridade "indefinida", pede mais detalhes |
| T03 | passou | Prioridade alta |
| T04 | parcial | Prioridade "indefinida" (melhorou), mas ainda não aponta a contradição nem pede esclarecimento |
| T05 | passou | "Fora do escopo", sem inventar data ou valor |
| T06 | passou | "Indefinida", sem inventar significado para o código 7731 |

**Resultado:** 5 passaram, 1 parcial (T04).

### v3
Ainda não realizada. Ponto a atacar: T04, para o prompt apontar a inconsistência do relato.

## Limitações conhecidas
- Cada chamado foi testado **uma vez** por versão. Não se sabe se a resposta é estável entre execuções.
- Apenas 6 chamados fictícios e um único modelo de IA.
- A v2 produziu justificativas mais longas que o pedido de "justificativa curta".
- Na v2 coletada, as saídas aparecem terminadas em `;` e `.` depois do JSON. Se isso vier da IA, o JSON não é válido para uso direto em automação (Projeto 1) e precisa ser corrigido.
- O prompt classifica, mas não gera a pergunta de esclarecimento que T02, T04 e T06 pedem (isso é papel do prompt 05).
