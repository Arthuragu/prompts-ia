# Prompt 01, v2: saída bruta

Saída recebida, uma por chamado, na ordem T01 a T06. Os `;` e o `.` depois das chaves foram copiados como vieram: se foram gerados pela IA, a saída não é JSON válido (ver limitações na ficha).

```text
T01
{
"categoria": "conectividade de rede",
"prioridade": "média",
"justificativa": "O tablet de pedidos apresenta falta de conexão desde as 11h, comprometendo potencialmente a operação da loja. Como o Wi-Fi do celular do gerente funciona normalmente e o tablet já foi reiniciado duas vezes sem sucesso, o problema aparenta estar relacionado à conexão ou configuração de rede do próprio dispositivo. A prioridade é média, pois há impacto operacional, mas não há informações suficientes para confirmar a extensão do problema ou se todos os pedidos estão sendo afetados."
};

T02
{
"categoria": "indefinida",
"prioridade": "indefinida",
"justificativa": "O chamado informa apenas que algo não está funcionando, sem identificar o equipamento, sistema ou serviço afetado, nem descrever o problema. Não há informações suficientes para determinar uma categoria técnica ou avaliar a prioridade. É necessário solicitar mais detalhes ao usuário."
};

T03
{
"categoria": "impressora",
"prioridade": "alta",
"justificativa": "A impressora de pedidos está offline durante o horário de almoço, impedindo a impressão dos pedidos e causando impacto direto na operação da loja. Pelo menos 5 pedidos já foram perdidos, caracterizando uma situação crítica que exige atendimento imediato."
};

T04
{
"categoria": "acesso ao aplicativo",
"prioridade": "indefinida",
"justificativa": "O usuário relata que não consegue abrir o aplicativo do entregador, embora tenha realizado entregas normalmente no dia anterior e ainda consiga visualizar seus pedidos na tela. Não há informações suficientes para identificar a causa da falha ou determinar a gravidade e o impacto operacional do problema."
};

T05
{
"categoria": "fora do escopo",
"prioridade": "indefinida",
"justificativa": "O chamado trata de uma dúvida sobre o prazo de repasse de valores por entregas realizadas, relacionada a pagamentos ou financeiro, e não a suporte técnico. Não há informações sobre a plataforma ou o calendário de pagamentos."
};

T06
{
"categoria": "indefinida",
"prioridade": "indefinida",
"justificativa": "O chamado informa apenas a ocorrência do erro 7731, sem identificar o sistema, aplicativo ou equipamento em que ele aparece. O código isolado não permite determinar com segurança a causa nem indicar um procedimento correto de resolução. É necessário identificar o sistema afetado e obter mais detalhes sobre o contexto do erro antes de classificá-lo tecnicamente ou definir sua prioridade."
}.
```
