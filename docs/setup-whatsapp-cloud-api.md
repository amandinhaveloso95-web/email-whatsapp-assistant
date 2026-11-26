# Setup da WhatsApp Cloud API (Meta)

Passo a passo resumido e as armadilhas que já encontramos.

## Passos

1. Criar conta em [Meta for Developers](https://developers.facebook.com/) e um portfólio empresarial. A verificação da empresa pode ficar para depois.
2. Criar um app com o caso de uso de conexão com clientes pelo WhatsApp.
3. Pegar, na tela do WhatsApp do app, o **Phone Number ID** e o **WhatsApp Business Account ID** do número de teste gratuito da Meta.
4. Adicionar o seu número pessoal como **destinatário de teste** e confirmar o código recebido.
5. Enviar uma mensagem de teste pela API para confirmar que funciona.
6. Configurar o webhook (veja abaixo) e assinar o campo `messages`.
7. Para uso real, registrar um número definitivo e gerar um token permanente.

## Armadilhas

**Perfil do número de teste não pode ser editado.** Nome e foto ficam fixos como "Test Number". Nome personalizado e ícone de robô só são possíveis com um número definitivo.

**Número definitivo.** Precisa ser um número que nunca teve conta de WhatsApp ativa (ou que teve a conta excluída antes do registro). Um chip pré-pago novo resolve. A verificação é por SMS ou ligação.

**Token temporário expira em 24 h.** Serve só para desenvolvimento. Para produção, crie um *System User* no Business Manager e gere um token permanente.

**Verificação do webhook (GET).** Quando você salva a URL de callback, a Meta faz um GET com `hub.mode`, `hub.verify_token` e `hub.challenge`. O seu endpoint precisa:

- comparar `hub.verify_token` com o token combinado;
- responder **200** com o valor de `hub.challenge` como corpo, sem aspas nem JSON;
- responder 403 se o token não bater.

Teste antes de salvar na Meta, abrindo no navegador:
`https://SEU-DOMINIO/webhook?hub.mode=subscribe&hub.verify_token=SEU_TOKEN&hub.challenge=123`
A resposta deve ser exatamente `123`.

**Webhook duplicado no n8n.** Dois nós Webhook com o mesmo caminho impedem a ativação do workflow, e um deles pode ficar escondido atrás do outro no canvas. Se o workflow não ativa por conflito de caminho, procure nós sobrepostos.

**URL de teste x produção (n8n).** Use a URL de **produção** no cadastro da Meta, com o workflow publicado e ativo.

**Janela de 24 h e templates.** Mensagens livres só podem ser enviadas depois que o usuário escreveu nas últimas 24 h. Para avisar sobre um e-mail novo fora dessa janela, é preciso um template aprovado. Veja [custos.md](custos.md).

**Limites das mensagens interativas.** Até 3 botões de resposta por mensagem, título de botão com até 20 caracteres, ID de botão com até 256 caracteres. Listas aceitam até 10 itens.

## Variáveis necessárias

Veja [.env.example](../.env.example). Nunca versione os valores reais.
