# 03. Resumir um problema

## Objetivo
Transformar uma conversa longa de um chamado em um resumo curto para quem assume o atendimento, sem precisar ler tudo.

## Entrada
Histórico de mensagens do chamado (conversas de [`testes/conversas-ficticias.md`](../../testes/conversas-ficticias.md)).

## Saída esperada
Resumo com três campos: **Problema**, **O que já foi tentado** e **Situação atual** (resolvido, não resolvido ou aguardando informação). Usa só o que está na conversa, sem inventar, e não repete dados pessoais ou senhas.

## Prompt (versão atual)
Versão atual: **v3**.

```
Resuma o chamado abaixo para o próximo atendente.
Regra de fidelidade: utilize somente informações e fatos que estejam explicitamente presentes na conversa. Não tire conclusões, não faça suposições e não acrescente recomendações, diagnósticos ou informações que não tenham sido mencionados pelos participantes.
Formato obrigatório: organize todo resumo utilizando exatamente os três campos abaixo:

* Problema: descrição objetiva do problema relatado.
* O que já foi tentado: procedimentos e ações realizados durante o atendimento. Se nada tiver sido tentado, informe isso.
* Situação atual: informe se o chamado está Resolvido, Não resolvido ou Aguardando informação, de acordo com o que foi explicitamente informado na conversa.
```

## Exemplo de uso
**Entrada:** conversa C5 (app de pedidos travando no tablet, com cinco procedimentos tentados).

**Saída obtida (v3):**
> * Problema: Aplicativo de pedidos da Loja Sabor Mineiro trava no tablet, especificamente ao abrir pedidos com mais de 5 itens.
> * O que já foi tentado: Fechar e abrir o aplicativo, reiniciar o tablet, limpar o cache, atualizar o aplicativo e reinstalá-lo. Após a reinstalação, o gerente conseguiu acessar novamente.
> * Situação atual: Não resolvido. O aplicativo continua travando ao abrir pedidos com mais de 5 itens.

Todos os resumos de cada versão estão em [`resultados/`](resultados/).

## Histórico de versões
Critério: "passou" quando o comportamento esperado da conversa (em `testes/conversas-ficticias.md`) foi cumprido; critérios secundários aparecem como ressalva.

### v1
**Prompt:**
```
Resuma o chamado abaixo para o próximo atendente.
```

**O que testei:** as 6 conversas fictícias, uma por vez. Resumos em [`resultados/v1.md`](resultados/v1.md).

| Conversa | Resultado | Observação |
|---|---|---|
| C1 | passou | Problema, causa (senha do Wi-Fi trocada) e solução. Ressalva: não confirma que os pedidos voltaram a chegar |
| C2 | passou | Usou a informação final (Wi-Fi, sem cabo, luz laranja) e registrou a correção. Status "não resolvido" |
| C3 | passou | Não inventou o modelo do celular; deixou claro o que falta |
| C4 | parcial | Título afirma "repasse atrasado", conclusão que não está na conversa. Acrescentou "próxima ação recomendada", incluindo informar "uma previsão concreta", e ficou bem mais longo |
| C5 | passou | Listou todos os passos tentados e o novo achado. Ressalva: sugeriu "falha no processamento", hipótese que não está na conversa |
| C6 | passou | Não repetiu CPF nem senha; resolvido |

**Resultado:** 5 passaram, 1 parcial (C4).

**O que saiu errado:**
1. Em C4 (e levemente em C5) a IA foi além da conversa: tirou conclusões ("atrasado", "falha no processamento") e fez recomendações que ninguém pediu.
2. O formato variou entre os resumos (prosa em quatro, tópicos em C4, títulos diferentes), o que atrapalha o uso automático no Projeto 1.

### v2
**O que mudei e por quê:** acrescentei uma única regra, a "regra de fidelidade": usar somente fatos explícitos na conversa, sem conclusões, suposições ou recomendações. Ataca o erro 1 da v1.

**Prompt:**
```
Resuma o chamado abaixo para o próximo atendente.
Regra de fidelidade: utilize somente informações e fatos que estejam explicitamente presentes na conversa. Não tire conclusões, não faça suposições e não acrescente recomendações, diagnósticos ou informações que não tenham sido mencionados pelos participantes.
```

**O que testei:** as mesmas 6 conversas. Resumos em [`resultados/v2.md`](resultados/v2.md).

| Conversa | Resultado | Observação |
|---|---|---|
| C1 | passou | Confirma que os pedidos voltaram a chegar |
| C2 | passou | Registrou as duas correções (cabo para Wi-Fi, vermelho para laranja) |
| C3 | passou | Sem invenções. Ressalva: não diz explicitamente que aguarda o entregador |
| C4 | passou | Sumiram o "atrasado" e as recomendações; resumo curto |
| C5 | passou | Sumiu a hipótese "falha no processamento". Ressalva: não declara a situação atual |
| C6 | passou | Sem CPF nem senha |

**Resultado:** 6 passaram.

**Efeito colateral:** a regra de fidelidade eliminou também as linhas de status ("Status:", "Resolvido") que a v1 trazia. Em C3 e C5, o resumo deixou de dizer a situação atual. Como só uma coisa mudou, o efeito pode ser atribuído a ela.

### v3
**O que mudei e por quê:** acrescentei um formato obrigatório com três campos (Problema, O que já foi tentado, Situação atual com três opções), para resolver o status ausente e deixar a saída previsível para uso automático.

**Prompt:** ver "Prompt (versão atual)" acima.

**O que testei:** as mesmas 6 conversas. Resumos em [`resultados/v3.md`](resultados/v3.md).

| Conversa | Resultado | Observação |
|---|---|---|
| C1 | passou | Status "Resolvido" explícito. Ressalva leve: "impedindo o recebimento de pedidos" é uma inferência |
| C2 | parcial | Todos os fatos e correções estão certos, mas o status "Aguardando informação" é discutível: ninguém estava esperando informação do gerente, a conversa só terminou sem solução. "Não resolvido" descreveria melhor |
| C3 | passou | "Aguardando informação" correto, com o que falta |
| C4 | passou | "Não resolvido", com o status "em processamento" |
| C5 | passou | "Não resolvido", com a pista (trava com mais de 5 itens) |
| C6 | passou | "Resolvido", sem CPF nem senha |

**Resultado:** 5 passaram, 1 parcial (C2).

**O que saiu errado:** o formato resolveu a variação e o status ausente, mas a lista fechada de três situações forçou uma escolha ruim em C2. É o mesmo padrão visto no prompt 01: quando o prompt obriga a escolher, a IA escolhe mesmo sem uma opção boa.

## Versão adotada
A **v3**, porque o formato fixo (campos e status explícitos) é o que o Projeto 1 precisa, mesmo com o erro de status em C2. A v2 acertou todo o conteúdo, mas sem status.

## Limitações conhecidas
- Cada conversa foi testada **uma vez** por versão; a estabilidade entre execuções não foi medida.
- 6 conversas fictícias e um único modelo de IA. A v1 já passou em 5 de 6, então o conjunto provavelmente é fácil.
- O status da conversa C2 ainda é classificado de forma discutível ("Aguardando informação" em vez de "Não resolvido").
- A avaliação é do próprio autor, comparando com o comportamento esperado de cada conversa.

## Melhoria futura
Esclarecer no prompt quando usar "Aguardando informação" (só quando o atendente pediu algo e a resposta não chegou) e quando usar "Não resolvido".
