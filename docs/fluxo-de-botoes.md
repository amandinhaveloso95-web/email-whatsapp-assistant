# Fluxo de botões

Telas em camadas. O WhatsApp permite no máximo 3 botões de resposta por mensagem. Quando houver mais opções, use **lista interativa**.

## Tela 1: notificação

```
🔴 Prioridade alta
De: Fulano <fulano@exemplo.com>
Assunto: Contrato para assinatura até sexta

[ Analisar ]  [ Abrir e-mail ]
```

- Emoji de prioridade sempre no começo (🔴 alta, 🟡 média, 🟢 baixa).
- E-mails da mesma conversa são agrupados em uma só notificação.

## Tela 2: resumo da IA

```
Resumo
• Pede assinatura do contrato anexo
• Prazo: sexta-feira
Ação necessária: assinar e devolver

[ Sugerir resposta ] [ Criar tarefa ]
[ Mais opções ▾ ]
```

"Mais opções" abre uma lista: Agendar reunião, Excluir, Abrir original.

## Tela 3a: rascunho de resposta

```
Rascunho:
"Olá Fulano, recebi o contrato e devolvo assinado até quinta. Obrigada!"

[ Enviar ] [ Outra versão ] [ Cancelar ]
```

- **Editar**: o WhatsApp não tem edição inline. A pessoa responde à mensagem do assistente com o texto novo, e o assistente mostra o rascunho atualizado para confirmar.
- **Enviar** sempre pede esse último clique. Nada sai sozinho.

## Tela 3b: reunião

`[ Ver horários livres ] [ Confirmar ] [ Não agendar ]`

## Tela 3c: tarefa

`[ Adicionar ] [ Ajustar prazo ] [ Não adicionar ]`

## Tela 3d: excluir

Confirmação extra antes de mover o e-mail para a lixeira: `[ Sim, excluir ] [ Cancelar ]`. Prefira lixeira a exclusão permanente.

## Regras

- Sem interação por 24 h, o pedido expira em silêncio (status `expirado`).
- IDs de botão: `<acao>:<chave curta>`, por exemplo `resumir:k7f3`. Título do botão com até 20 caracteres.
- Todo clique é registrado na tabela de estado antes de executar a ação, para evitar execução em duplicidade se o webhook for reenviado.
