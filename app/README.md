# Central de E-mails (app para Outlook)

Versão em app do assistente: em vez de receber os e-mails no WhatsApp, você os vê como **mensagens de uma conversa**, com os mesmos botões do fluxo original.

É um arquivo único (`index.html`) feito para rodar como **artefato do Claude**, ligado ao conector **Microsoft 365** (Outlook). Não tem servidor nem chave de API: a leitura da caixa e a IA passam pelo Claude do próprio usuário.

## O que faz

- Lê a caixa de entrada e confere novos e-mails a cada 30 s a 5 min, enquanto o app está aberto.
- Cada e-mail vira um balão com **Abrir e-mail** e **Resumir**.
- O resumo traz pontos principais, o que fazer e prazo, e oferece **Sugerir resposta**, **Adicionar às tarefas**, **Ler e-mail completo** e **Excluir**.
- A resposta tem 4 tons e é editável. Só vira **rascunho no Outlook**: o app nunca envia sozinho.
- Excluir move para Itens Excluídos, com confirmação.
- Respostas de reunião (aceito, recusado, provisório) ficam ocultas, exceto as que têm comentário escrito. Dá para mudar em Configurações.
- Extras: pergunta livre sobre os e-mails, prioridade por IA, resumo do dia, VIPs e silenciar remetentes, busca, filtros, modo escuro.
- Sem conector (por exemplo, abrindo o arquivo direto no navegador), roda em **modo demonstração** com e-mails fictícios.

## Como usar

1. Ligue o conector Microsoft 365 na sua conta do Claude.
2. Peça ao Claude para publicar `index.html` como artefato (um arquivo HTML, com os recursos `mcp`, `sample`, `db` e `user` declarados e as ferramentas `outlook_email_search`, `read_resource`, `outlook_create_reply_draft` e `outlook_trash_thread` do servidor "Microsoft 365").
3. Abra o artefato, vá em Configurações e preencha seu contexto (profissão) e a assinatura das respostas.

## Privacidade

- O código não contém dados pessoais. Nome, contexto e assinatura são configurados por quem usa e ficam salvos na conta do usuário (ou só no navegador, se não houver banco).
- Para resumir ou responder, o texto do e-mail é enviado ao Claude. Não use com e-mails que não possam ser processados assim.
- O app nunca envia e-mails e não manipula senhas.

## Limites

- Só avisa com o app aberto. Aviso com tudo fechado exige serviço externo (Power Automate, bot de Telegram).
- Mostra os 25 e-mails mais recentes e carrega mais sob demanda.
