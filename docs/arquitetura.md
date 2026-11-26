# Arquitetura

Quatro camadas independentes. Cada uma pode ser trocada sem mexer nas outras.

## 1. Entrada (e-mail)

- **Gmail**: gatilho de novo e-mail (push ou consulta a cada poucos minutos).
- **Outlook / Microsoft 365**: segundo gatilho, alimentando o mesmo fluxo. Contas institucionais costumam exigir aprovação de TI para registrar o app, por isso o MVP começa no Gmail pessoal.
- Cada conta tem seu próprio gatilho; tudo converge para o mesmo formato interno (`remetente`, `assunto`, `corpo`, `thread_id`, `message_id`, `conta`).

## 2. Cérebro (IA)

Recebe o e-mail já limpo (veja segurança) e devolve **JSON com formato fixo** ([schemas/analise.schema.json](../schemas/analise.schema.json)):

- `prioridade`: alta, média ou baixa
- `resumo`: pontos principais, objetivo
- `acao_necessaria`: o que a pessoa precisa fazer, se houver
- `prazo`: data citada no e-mail, se houver
- `tipo`: `responder`, `tarefa`, `reuniao` ou `informativo`

O `tipo` decide quais botões aparecem. Um e-mail informativo não precisa do botão "Criar tarefa".

## 3. Interação (canal de mensagens)

Um *adaptador* por canal, todos com a mesma interface (`enviarTexto`, `enviarBotoes`, `enviarLista`, `receberClique`):

| Canal | Botões | Observação |
|---|---|---|
| WhatsApp Cloud API (Meta) | até 3 botões de resposta ou lista com até 10 itens | cobrança por mensagem, veja [custos.md](custos.md) |
| Telegram Bot API | botões inline sem limite prático | gratuito |

Cada botão carrega só um **ID curto** (ex.: `resumir:k7f3`). O ID de botão tem limite de tamanho, então o conteúdo do e-mail nunca vai dentro do botão.

## 4. Estado

Tabela simples (planilha, Data Table do n8n, D1 ou SQLite):

| campo | exemplo |
|---|---|
| `chave` | `k7f3` |
| `message_id` / `thread_id` | ids do provedor de e-mail |
| `resumo`, `rascunho` | texto gerado |
| `status` | `novo`, `resumido`, `rascunhado`, `tarefa_criada`, `expirado` |
| `criado_em` | para o timeout de 24 h |

Sem essa tabela, o clique no botão não sabe a qual e-mail se refere.

## Decisões já tomadas

- Começar pelo Gmail e deixar o Outlook para a segunda fase.
- Usar a API oficial da Meta em vez de soluções não oficiais baseadas em QR code, porque botões interativos só são confiáveis na API oficial.
- Mensagens vêm de uma **identidade própria do assistente**, não do número pessoal, com nome e ícone de robô. Isso também permite compartilhar o sistema com outras pessoas depois.
- Rascunho de resposta nunca é enviado sem clique em "Enviar".

## Ideias para depois

- Aprender o estilo de escrita da pessoa comparando o rascunho da IA com a versão que ela realmente enviou. Guardar só padrões de escrita, nunca o conteúdo de e-mails de terceiros.
- Resumo diário consolidado, separado das notificações em tempo real.
- Agendamento de reunião com sugestão de horários livres do calendário.
- Regras por remetente (sempre alta prioridade, nunca notificar).
