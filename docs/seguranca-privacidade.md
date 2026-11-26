# Segurança e privacidade

O assistente lê e-mails, que costumam conter dados de terceiros. Trate isso com cuidado desde o início.

## Antes de enviar o e-mail para a IA

Passe o texto por um filtro simples (expressões regulares) que remove ou mascara:

- códigos de verificação (OTP) e senhas
- chaves de API e tokens
- números de cartão e documentos de identificação

Se a caixa estiver vazia ou o e-mail não passar nas regras de notificação, **nem chame a IA**. Isso economiza custo e reduz exposição.

## Segredos

- Tokens, chaves e IDs de conta ficam em variáveis de ambiente ou no cofre da plataforma, nunca no código nem em workflows exportados.
- Antes de exportar um workflow para versionar, abra o JSON e remova IDs de credenciais, URLs privadas e números de telefone.
- Troque qualquer token que tenha sido colado em chat, issue ou commit por engano.

## Dados guardados

- A tabela de estado guarda só o necessário para os botões funcionarem e **expira** (24 h sem interação).
- Para aprender o estilo de escrita, guarde apenas padrões (tom, saudações, fechamentos), nunca o conteúdo de e-mails de outras pessoas.

## Ações destrutivas

- Excluir e-mail: confirmação extra e preferência pela lixeira.
- Enviar resposta: só depois do clique em "Enviar".
- A IA nunca age sozinha sobre a caixa de entrada.

## Multiusuário

Se o sistema for compartilhado com outras pessoas, cada uma precisa da própria autorização OAuth do e-mail e do próprio estado isolado. Não misture contas na mesma tabela sem uma coluna de dono.
