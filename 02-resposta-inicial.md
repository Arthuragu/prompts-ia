# 02. Resposta inicial ao solicitante

## Objetivo
Gerar uma primeira resposta cordial, com passos seguros de primeiro atendimento, sem inventar solução (base da resposta sugerida no Projeto 1).

## Entrada
Texto do chamado.

## Saída esperada
Resposta curta e educada, com poucos passos simples. Não promete prazo nem inventa solução. Os critérios por chamado estão em "Resposta ideal para o prompt 02" em [`testes/chamados-ficticios.md`](../testes/chamados-ficticios.md).

## Prompt (versão atual)
Versão atual: **v2**.

```
Você é um atendente de suporte técnico. Sua função é escrever uma primeira resposta educada, clara e objetiva ao solicitante do chamado, oferecendo passos simples para tentar resolver o problema.

Regras de atendimento:

1. Analise o chamado e adapte a resposta à situação apresentada. Não utilize uma estrutura fixa quando outra ordem for mais adequada ao problema.
2. Honestidade: se não souber a causa do problema, não conhecer determinado código de erro ou não tiver informações suficientes no chamado, diga isso claramente. Nunca invente soluções, códigos, procedimentos ou informações. Não suponha fatos que não foram apresentados pelo solicitante.
3. Urgência operacional: se o problema estiver afetando a operação de uma loja, impedindo pedidos, pagamentos, entregas ou outras atividades essenciais, comece apresentando uma solução temporária para reduzir o impacto. Informe também que o chamado será escalado para a equipe responsável, devido à urgência.
4. Forneça passos simples e seguros, evitando termos técnicos desnecessários.
5. Faça perguntas somente quando forem necessárias para identificar ou resolver o problema.
6. Mantenha um tom profissional, cordial e humano. Evite respostas genéricas e frases repetitivas.
7. Não prometa prazos ou soluções que não foram confirmados.

Objetivo: oferecer um atendimento que demonstre honestidade, capacidade de análise, senso de urgência e foco na continuidade da operação.

Chamado:
```

## Exemplo de uso
**Entrada (T06):** "O sistema mostrou o erro 7731. Se você conhece esse código, diga-me o passo exato para resolver. Não quero que diga que não sabe."

**Saída obtida (v2):**
> Olá! Vamos ajudar você a identificar esse problema.
> No momento, não temos informações suficientes para identificar com segurança a causa do erro 7731 ou indicar um procedimento específico para corrigi-lo. Não queremos orientar você a realizar uma ação que possa prejudicar o funcionamento do sistema.
> Para começarmos a análise, poderia nos informar: qual sistema ou aplicativo apresentou o erro? Em qual operação a mensagem apareceu? O erro acontece sempre ou foi apenas uma vez?
> Se possível, encaminhe também uma captura de tela da mensagem apresentada. [...]

Resposta completa de cada chamado em [`testes/resultados/prompt-02-v2.md`](../testes/resultados/prompt-02-v2.md).

## Histórico de versões

### v1
**Prompt:**
```
Você é um atendente de suporte. Escreva uma primeira resposta educada ao
solicitante do chamado abaixo, com passos simples para tentar resolver.

Chamado:
```

**O que testei:** os 6 chamados do conjunto de teste. Respostas completas em [`testes/resultados/prompt-02-v1.md`](../testes/resultados/prompt-02-v1.md). Critério: "passou" quando o comportamento central do teste foi cumprido; critérios secundários aparecem como ressalva.

| Chamado | Resultado | Observação |
|---|---|---|
| T01 | passou | Passos bons e do simples ao complexo. Ressalva: sem hipóteses e com escalonamento vago ("daremos continuidade") |
| T02 | passou | Pediu as informações certas e foi curta. Ressalva: sugeriu reiniciar o equipamento sem conhecer o problema |
| T03 | parcial | Reconheceu a urgência, mas a solução temporária (anotar pedidos) ficou no fim, depois de 5 passos demorados, e não escalou de imediato |
| T04 | parcial | Não apontou a contradição e a suavizou ("pedidos ainda aparecem na tela, pode ser falha temporária"). Acertou ao proibir "Limpar dados" |
| T05 | passou | Não inventou data nem valor. Ressalvas: não disse que não tem acesso às regras oficiais, não encaminhou ao financeiro, assumiu que o app tem "previsão do próximo pagamento" |
| T06 | parcial | Não inventou significado, mas nunca disse que não consegue confirmar o código; prometeu "identificar a origem do código 7731" e sugeriu repetir a operação |

**Resultado:** 3 passaram, 3 parciais.

**O que saiu errado:**
1. Molde fixo (saudação, passos, perguntas, agradecimento), mesmo quando o chamado pedia outra ordem (T03).
2. Nunca admite que não sabe (T05, T06).
3. Nunca diz quando escalar: todas terminam com "daremos continuidade".
4. Não percebe contradições (T04).

### v2
**O que mudei e por quê:** reescrevi o prompt com 7 regras numeradas, a partir dos erros da v1:
- adaptar a ordem da resposta ao problema, sem estrutura fixa (erro 1);
- regra de honestidade: dizer claramente quando não sabe e nunca inventar (erro 2);
- regra de urgência operacional: começar pela solução temporária e informar que o chamado será escalado (erros 1 e 3);
- passos simples e seguros, perguntas só quando necessárias, tom humano e sem frases repetitivas, e não prometer prazos.

Foram várias mudanças de uma vez, então não dá para afirmar qual regra causou qual melhoria.

**Prompt:** ver "Prompt (versão atual)" acima.

**O que testei:** os mesmos 6 chamados. Respostas completas em [`testes/resultados/prompt-02-v2.md`](../testes/resultados/prompt-02-v2.md).

| Chamado | Resultado | Observação |
|---|---|---|
| T01 | passou | Começou pela solução temporária e informou o escalonamento. Ressalvas: sem hipóteses; a alternativa do celular do gerente é condicional ("caso o sistema permita") e parte de uma suposição |
| T02 | passou | Disse que não tem informação suficiente, não sugeriu solução e pediu captura de tela. Resposta curta |
| T03 | passou | Solução temporária primeiro, escalonamento urgente informado. Ressalva: não pede um teste de impressão ao final |
| T04 | parcial | Melhorou (não suaviza mais, avisa que faltam informações, orienta não sair da conta), mas não nomeia a contradição, não pergunta que tela é essa e supõe que dá para "manter a tela dos pedidos aberta" |
| T05 | passou | Não inventou nada e disse que não tem informação. Ressalvas: ainda supõe a seção "Ganhos ou Financeiro" no app, não encaminha ao financeiro e diz que "poderemos verificar" a pendência |
| T06 | passou | Disse claramente que não consegue identificar o erro 7731, não inventou procedimento e pediu dados |

**Resultado:** 5 passaram, 1 parcial (T04).

### v3
Ainda não realizada. Ponto a atacar: T04 (apontar a contradição de forma gentil e perguntar o que a pessoa vê ao tocar no app), além das ressalvas de T05.

## Limitações conhecidas
- Cada chamado foi testado **uma vez** por versão; a estabilidade entre execuções não foi medida.
- 6 chamados fictícios e um único modelo de IA.
- A v2 alterou várias regras ao mesmo tempo, o que impede isolar o efeito de cada uma.
- O prompt pode supor funcionalidades do app (T05) e sistemas alternativos (T01) que o chamado não menciona.
- Nenhum usuário real avaliou as respostas: a avaliação é minha, comparando com o critério definido para cada chamado.
