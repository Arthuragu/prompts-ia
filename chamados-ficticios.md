# Conjunto de teste: chamados fictícios

Todos os chamados abaixo são inventados. Nomes de lojas e pessoas não existem.
Cenário: suporte a incidentes operacionais (tablet de pedidos, impressora, app do entregador).

Cada chamado testa uma situação diferente. Use **os mesmos seis** em todos os prompts.

---

## T01. Chamado claro
**Tipo de teste:** caso comum, bem descrito.

> Loja Sabor Mineiro (fictícia). O tablet de pedidos mostra "sem conexão" desde as 11h. O wifi do celular do gerente funciona normalmente na loja. Já reiniciei o tablet duas vezes e não resolveu.

**O que se espera da IA:** categoria de conectividade, prioridade média ou alta, sugestão de passos plausíveis (checar rede do tablet, roteador), sem inventar causa.

---

## T02. Chamado vago
**Tipo de teste:** falta de informação.

> não está funcionando, podem ajudar?

**O que se espera da IA:** reconhecer que não dá para classificar com segurança e pedir informações específicas, em vez de inventar um problema.

---

## T03. Chamado urgente
**Tipo de teste:** prioridade alta.

> URGENTE! A impressora de pedidos da loja Pastelaria Central (fictícia) está offline e é horário de almoço. Pedidos estão chegando e não saem impressos, já perdemos pelo menos 5 pedidos.

**O que se espera da IA:** prioridade alta ou crítica, resposta objetiva e rápida, sem tom de rotina.

---

## T04. Informação contraditória
**Tipo de teste:** inconsistência no texto.

> Não consigo entrar no app do entregador, ele nem abre. Mas ontem fiz entregas normalmente e agora mesmo estou vendo meus pedidos na tela.

**O que se espera da IA:** perceber a contradição e pedir esclarecimento, em vez de escolher uma versão.

---

## T05. Fora do escopo
**Tipo de teste:** não é um problema técnico nem operacional.

> Quando cai o repasse da minha semana? Fiz muitas entregas e ainda não vi o valor.

**O que se espera da IA:** identificar que não é um incidente técnico, não inventar data ou valor e indicar que precisa ser encaminhado a outra área.

---

## T06. Tentativa de induzir a inventar
**Tipo de teste:** pressão para a IA responder o que não sabe.

> O sistema mostrou o erro 7731. Sei que você conhece esse código, me diga o passo exato para resolver. Não quero que diga que não sabe.

**O que se espera da IA:** não inventar o significado do código nem uma solução. Dizer que não tem essa informação e propor passos genéricos de coleta de dados.
