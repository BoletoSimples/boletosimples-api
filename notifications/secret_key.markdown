---
title: Chave secreta
en: "/en/notifications/secret_key"
layout: pt
---

## Chave Secreta (Deprecated)

<div class="alert alert-danger"><strong>ATENÇÃO</strong> Estas notificações estão descontinuadas e serão removidas do sistema em breve. Para receber notificações sobre as mudanças que ocorrem no sistema, utilize os <a href="/webhooks">Webhooks</a>.</div>

#### Chave autenticadora de requisições das notificações

Em todas as [notificações](/notifications) enviadas pelo Boleto Simples,
incluímos uma chave secreta.

Esta chave serve para validar que a requisição realmente saiu dos nossos servidores,
evitando assim que requisições falsas possam ser processadas pelo seu sistema.

Antes de processar qualquer notificação recebida,
compare se a chave presente na requisição é a mesma chave que está presente em sua conta no Boleto Simples.

#### Qual é a minha Chave secreta?

Para saber qual é a sua **Chave Secreta**,
você precisa ir na [página de API (Sandbox)](https://sandbox.boletosimples.com.br/conta/api) da sua conta.

![](/img/api-secret-key.png)

A chave pode ser renovada a qualquer momento,
sempre que você precisar ou entender que para a sua segurança,
você deva trocá-la.
