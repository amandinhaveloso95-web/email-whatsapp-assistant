# Custos e como chegar a zero

Levantamento feito em novembro de 2026. Preços e limites mudam, confira as fontes antes de decidir.

## Onde está o custo

| Peça | Opção paga | Opção gratuita | Observação |
|---|---|---|---|
| Automação | n8n Cloud, a partir de cerca de US$ 20/mês, com limite de execuções | n8n Community Edition **auto-hospedada** | O software é gratuito, mas precisa de um servidor seu e de manutenção |
| Servidor | VPS pago | Máquina própria, ou código próprio em Cloudflare Workers (plano Free) | Veja abaixo |
| Canal | WhatsApp Cloud API | **Telegram Bot API** | O WhatsApp passou a cobrar por mensagem, veja abaixo |
| IA | Modelos pagos por uso | Camadas gratuitas de alguns provedores | Confira os limites atuais do provedor escolhido |
| E-mail e calendário | Gmail API e Google Calendar API | mesmas | Uso pessoal costuma caber nas cotas gratuitas |

## n8n

- Não existe plano gratuito na nuvem do n8n; o que é gratuito é a Community Edition, que você hospeda ([fonte](https://www.activepieces.com/blog/n8n-free-plan-in-2026-community-edition-vs-cloud)).
- Na versão auto-hospedada não há cota de execuções, o limite é a máquina ([fonte](https://www.ssdnodes.com/learn/is-n8n-free-community-vs-enterprise)).
- A licença é *Sustainable Use*, não open source: pode hospedar para você ou sua equipe, mas **não** operar como serviço para clientes ([fonte](https://dev.to/beton/n8n-pricing-teardown-2026-4oa)). Se a ideia é compartilhar o sistema com outras pessoas, avalie isso antes de usar o n8n como base.

## Cloudflare Workers (código próprio)

Alternativa sem servidor para manter e sem licença restritiva, mas exige escrever código.

- Plano Free: 100.000 requisições por dia, 10 ms de CPU por requisição, 5 gatilhos de cron por conta ([limites](https://developers.cloudflare.com/workers/platform/limits)). Tempo esperando respostas de rede (Gmail, IA, Meta) não conta como CPU.
- KV gratuito: 100.000 leituras e 1.000 gravações por dia ([fonte](https://developers.cloudflare.com/kv/platform/pricing)).
- D1 gratuito: 500 MB por banco ([fonte](https://developers.cloudflare.com/d1/platform/limits)).
- O gatilho de novo e-mail seria um cron consultando a API do Gmail a cada poucos minutos.

## WhatsApp

Desde 1º de outubro de 2026 a Meta cobra por mensagem enviada pela empresa, inclusive respostas livres dentro da janela de 24 h e templates de utilidade ([fonte](https://developers.facebook.com/documentation/business-messaging/whatsapp/pricing/non-template-messages/)). Mensagens recebidas do usuário são gratuitas.

- Tarifa no Brasil informada pela Meta: **0,68 centavo de dólar por mensagem** (valor de 1º de julho de 2026).
- Conta rápida: 1.000 mensagens do assistente por mês ≈ US$ 6,80. Cada notificação, resumo e rascunho conta como uma mensagem.
- Mensagens proativas (novo e-mail chegando sem você ter escrito nas últimas 24 h) exigem **template aprovado** pela Meta.

Como gastar menos: notificar só prioridade média e alta, agrupar e-mails da mesma conversa, usar resumo diário para o resto.

## Telegram

A API de bots do Telegram não cobra por mensagem, aceita botões inline e não tem janela de 24 h nem templates. É a rota **totalmente gratuita** com a mesma experiência de botões.

## Recomendação

1. **Zero real**: Telegram + n8n auto-hospedado (ou Cloudflare Workers) + IA em camada gratuita.
2. **WhatsApp com custo baixo**: mesmo desenho, trocando só o adaptador de canal e aceitando uns poucos dólares por mês, controlados pelas regras de notificação acima.

Por isso a arquitetura separa o canal em um adaptador ([arquitetura.md](arquitetura.md)).
