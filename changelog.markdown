---
title: Changelog
position: 12
en: "/en/changelog"
layout: pt
---

## Últimas mudanças na API

#### Código fonte da documentação

A documentação da API é um [projeto público no Github](https://github.com/BoletoSimples/boletosimples-docs). Você pode acompanhar as mudanças na documentação na [página dos commits](https://github.com/BoletoSimples/boletosimples-docs/commits/master).

<!-- #### Receba as atualizações por e-mail

Você também pode se inscrever para receber as notificações de alterações da API por e-mail.

<form action="https://www.getdrip.com/forms/93702557/submissions" method="post" data-drip-embedded-form="93702557">
<input type="email" name="fields\[email\]" value="" required="required" placeholder="Seu e-mail" />
<input type="submit" name="submit" value="Inscrever" data-drip-attribute="sign-up-button" />
</form> -->

#### Últimas alterações realizadas na API.

### 15/07/2021

- Adicionado novo endpoint para [Download do CNAB de Retorno](/reference/v1/discharges/#download-do-cnab).

### 22/06/2021

- Ajusta documentação em [Webhook Enviados](/reference/v1/webhook_deliveries/)
- Ajusta documentação em [E-mails enviados](/reference/v1/email_deliveries/)
- Documenta o campo `resource_owner_id` em [Eventos](/reference/v1/events/)

### 11/06/2021

- Retiramos a documentação sobre o banco S4fr4 por solicitação do banco.

### 21/05/2021

- Remove obrigatoriedade do campo `description` em Boletos, Assinaturas e Carnês
- Remove campos descontinuados `interest_daily_percentage`, `interest_daily_value`, `interest_monthly_percentage`, `late_payment_interest`, `discount_limit_date`, `fine_for_delay` em Boletos, Assinaturas e Carnês
- Remove endpoints descontinuados `GET /api/v1/bank_billets/cnpj_cpf`, `GET /api/v1/bank_billets/our_number` e `GET /api/v1/bank_billets/status` e `POST /api/v1/bank_billets/bulk` em [Boletos](/reference/v1/bank_billets)
- Documenta os campos `customer_ignore_sms`, `customer_contact_person` e `payment_count` em [Boletos](/reference/v1/bank_billets)
- Documenta os campos `customer_ignore_sms`, `customer_contact_person`, `payment_count`, `days_for_sue`, `days_for_revoke` e `days_for_negativation` em [Assinaturas](/reference/v1/customer_subscriptions)
- Documenta os campos `customer_ignore_sms`, `customer_contact_person`, `payment_count`, `days_for_sue`, `days_for_revoke`, `days_for_negativation`, `document_date`, `document_type`, `document_number` e `custom_bank_billets` em [Carnês](/reference/v1/installments)

### 17/05/2021

- Adiciona informações sobre o [módulo TOTVS Microsiga Protheus](/modules/totvs-protheus)

### 13/05/2021

- Documenta o campo `allow_expiration_on_weekends` em [Carteiras de Cobrança](/reference/v1/bank_billet_accounts)

### 11/05/2021

- Adiciona os campos `pix_enabled` e `pix_qrcode` em [Boletos](/reference/v1/bank_billets)

- Adiciona o campo `paid_by_pix` em [Pagamentos de Boleto](/reference/v1/bank_billet_payments)

### 08/02/2021

- Atualiza slug de carteira `cecred-bs-1` para `ailos-bs-1` em [Ailos](/bank_contracts/ailos)

### 08/02/2021

- Atualiza o módulo do [Totvs RM](/modules/totvs-rm)

### 04/02/2021

- Adiciona os campos `guarantor_name`, `guarantor_cnpj_cpf`, `guarantor_zipcode`, `guarantor_address`, `guarantor_city_name`, `guarantor_state`, `guarantor_neighborhood`, `guarantor_address_number`, `guarantor_address_complement` e `guarantor_phone_number` em [Carnês](/reference/v1/installments)

- Adiciona os campos `guarantor_name`, `guarantor_cnpj_cpf`, `guarantor_zipcode`, `guarantor_address`, `guarantor_city_name`, `guarantor_state`,`guarantor_neighborhood`, `guarantor_address_number`, `guarantor_address_complement` e `guarantor_phone_number` em [Assinaturas](/reference/v1/customer_subscriptions)

### 02/02/2021

- Adiciona o campo `allow_expiration_on_weekends` em [Carteiras de Cobrança](/reference/v1/bank_billet_accounts)
- Documenta o campo `customer_ignore_email` em [Boletos](/reference/v1/bank_billets)
- Documenta o campo `customer_ignore_email` em [Carnês](/reference/v1/installments)
- Documenta o campo `customer_ignore_email` em [Assinaturas](/reference/v1/customer_subscriptions)
- Documenta o campo `ignore_email` em [Boletos](/reference/v1/bank_billets)
- Documenta o campo `ignore_email` em [Clientes](/reference/v1/customers)

### 28/01/2021

- Adiciona o campo `days_for_negativation` em [Boletos](/reference/v1/bank_billets/#days_for_negativation)

### 11/01/2020

- Depreciado o campo `default_to_import` em [Carteiras de Cobrança](/reference/v1/bank_billet_accounts)

### 08/01/2021

- Adiciona novo formato de endereço do beneficiário em [Carteiras de Cobrança](/reference/v1/bank_billet_accounts),
  a antiga maneira continua funcionando da mesma forma mas será depreciada.

### 30/12/2020

- Adiciona o campo `default_to_import` em [Carteiras de Cobrança](/reference/v1/bank_billet_accounts)

### 10/12/2020

- Adiciona campo `tags` em [Clientes](/reference/v1/customers)
- Adiciona filtro por `tags` nos [Clientes](/reference/v1/customers/#listar-clientes)
- Corrige erro de digitação do campo `nickname` em [Clientes](/reference/v1/customers)
- Endpoint de atualização dos [Clientes](/reference/v1/customers/#atualizar-cliente) não retorna conteúdo

### 04/12/2020

- Adiciona [módulo WHMCS](/modules/whmcs)

### 02/12/2020

- Documenta o campo `external_code` em [Clientes](reference/v1/customers/)
- Documenta o campo `custom_data` em [Boletos](/reference/v1/bank_billets/)

### 25/05/2020

- Adiciona [Política de Retenção de Dados](/data_retention)

### 30/04/2020

- Atualiza [documentação do Zapier](/integrations/zapier/) com as funções disponíveis na versão 2.0.0
- Remove eventos de webhook que não são mais usados.

### 16/04/2020

- Remove a documentação do campo `source_type` na [Importação de Boletos](/reference/v1/imports/bank_billets/)
- Melhora a documentação dos formatos de arquivos aceitos na [Importação de Boletos](/reference/v1/imports/bank_billets/)

### 02/04/2020

- Documenta `charge_type` em [Boletos](/reference/v1/bank_billets/#charge_type)
- Documenta `dispatch_type` em [Boletos](/reference/v1/bank_billets/#dispatch_type)
- Documenta `register_type` em [Boletos](/reference/v1/bank_billets/#register_type)

### 19/03/2020

- Documenta `split_payment` em [Boletos](/reference/v1/bank_billets/)
- Documenta `floating` em [Contas para Split](/reference/v1/bank_billets/#split_accounts)

### 16/03/2020

- Atualiza parâmentros de [Contas para Split](/reference/v1/bank_billets/#split_accounts)

### 31/01/2020

- Depreca o endpoint em [Criar boletos em lote](/reference/v1/bank_billets/#criar-boletos-em-lote)

### 21/01/2020

- Documenta o campo `created_from` e `created_to` em [Registro de Retorno](/reference/v1//webhook_deliveries/#reenviar-webhook)

### 10/01/2020

- Documenta [ABC](/bank_contracts/abc/)
- Documenta [ARBI](/bank_contracts/arbi/)
- Documenta [BIB](/bank_contracts/bib/)
- Documenta [BNP Paribas](/bank_contracts/bnpparibas/)
- Atualiza Documenta [Sofisa](/bank_contracts/sofisa/)

### 14/10/2019

- Altera nome da cooperativa CECRED para AILOS

### 14/10/2019

- Documenta o campo `credit_at` em [Registro de Retorno](/reference/v1/bank_billet_payments/)

### 03/10/2019

- Documenta [Relatórios](/reference/v1/reports)

### 27/09/2019

- Documenta filtro por `ID da Remessa` em [Registro de Remessa](/reference/v1/bank_billet_remittances/#listar-registros-de-remessa)
- Documenta novos eventos de usuários em [Eventos](/webhooks/events/)

### 09/08/2019

- Documenta filtro por `ID do Objeto` em [Webhooks enviados](/reference/v1/webhook_deliveries/#listar-webhook-enviados)

### 08/05/2019

- Atualiza lista de [Tipo de Documento](/reference/v1/bank_billets/#document_type)
- Remove status `downloaded` não utilizado em [Remessas](/reference/v1/remittances/#status)

### 30/04/2019

- Atualiza lista de ocorrências [Banrisul](/bank_contracts/banrisul/)

### 11/04/2019

- Adiciona filtro por [ID do Objeto](/reference/v1/email_deliveries/) nos emails enviados

### 11/04/2019

- Adiciona [tabela de códigos de ocorrência do Boleto Simples](/reference/v1/bank_billet_discharges/#our_occurrence)
- Documenta [Kind](/reference/v1/bank_billet_accounts/#kind) em Carteiras de Cobrança

### 10/04/2019

- Documenta [Caruana](/bank_contracts/caruana/)
- Documenta [CRESOL](/bank_contracts/cresol/)
- Documenta [Daycoval](/bank_contracts/daycoval/)
- Documenta [Sofisa](/bank_contracts/sofisa/)

### 09/04/2019

- Documenta [Registros de Boleto](/reference/v1/bank_billet_registrations)

### 25/03/2019

- Adicionado novo endpoint para [Excluir pendências](/reference/v1/bank_billet_remittances/#excluir-pendências).

### 25/02/2019

- Documenta o campo `line_parsed` em [Registro de Retorno](/reference/v1/bank_billet_discharges/)

### 20/02/2019

- Documenta o campo `truncated_address` em [Clientes](/reference/v1/customers)

### 13/02/2019

- Adiciona o campo `control_number` em [Boletos](/reference/v1/bank_billets/)
- Descontinuando o endpoint de filtro de [Boletos por status](/reference/v1/bank_billets/#buscar-por-situação-do-boleto)
- Descontinuando o endpoint de filtro de [Boletos por CPF/CNPJ](/reference/v1/bank_billets/#buscar-por-cpf-ou-cnpj)
- Descontinuando o endpoint de filtro de [Boletos por nosso número](/reference/v1/bank_billets/#buscar-por-nosso-número)

### 16/10/2018

- Documenta [Pagamentos de Boleto](/reference/v1/bank_billet_payments)
- Atualiza lista de [Eventos](/webhooks/events)

### 14/06/2018

- Documenta [E-mails enviados](/reference/v1/email_deliveries)
- Atualiza lista de carteiras do [Safra](/bank_contracts/safra)

### 21/05/2018

- Documenta [Cancelar boletos em lote](/reference/v1/bank_billets/#cancelar-boletos-em-lote).

### 07/05/2018

- Atualiza lista de carteiras do [Banco do Brasil](/bank_contracts/bb/)
- Atualiza lista de carteiras do [Itaú](/bank_contracts/itau/)

### 20/04/2018

- Documenta [Importações](/reference/v1/imports)

### 19/04/2018

- Documenta o campo `bank_billet_discharges` em [Retornos](/reference/v1/discharges)
- Remove o campo `bank_billets_with_transactions` em [Retornos](/reference/v1/discharges)
- Adicionado novo endpoint para [Reprocessar CNAB de Retorno](/reference/v1/discharges/#reprocessar-cnab).

### 19/02/2018

- Adicionado novo endpoint para [Criar boletos em lote](/reference/v1/bank_billets/#criar-boletos-em-lote).
- Adicionado tabela de [Ocorrências](/reference/v1/bank_billet_remittances/#criar-pendências) disponíveis em cada [banco](/bank_contracts/).
- Adicionado tabela com código de instruções de cobrança para [Itaú](/bank_contracts/itau/#códigos-de-instrução-de-cobrança)
- Inclui `first_instruction`, `second_instruction`, `sue_code` e `revoke_code` nos [Boletos](/reference/v1/bank_billets/)

### 22/01/2018

- Adicionado novos parâmetros ao endpoint para filtrar [Boletos](/reference/v1/bank_billets/#listar-boletos).

### 10/01/2018

- Adicionado novo parâmetro ao endpoint para criação de [Carnês](/reference/v1/installments): tags.

- Adicionado novo parâmetro ao endpoint para criação de [Assinaturas](/reference/v1/customer_subscriptions): tags.

### 02/01/2017

- Adicionado modelo de dados para [Tipos de documentos](/reference/v1/bank_billets/#document_type)

### 15/12/2017

- Adicionado endpoint de listar [Registro de Remessas](/reference/v1/bank_billet_remittances/#listar-registros-de-remessa) pendentes ou não pendentes

- Adicionado endpoint de listar apenas [Registro de Remessas](/reference/v1/bank_billet_remittances/#listar-registros-de-remessa-pendentes) pendentes

- Adicionado endpoint para criar [Registro de Remessas](/reference/v1/bank_billet_remittances/#criar-pend%C3%AAncias) a partir do código de operação banco

### 12/12/2017

- Adicionado novos parâmetros ao endpoint de filtro de [Boletos](/reference/v1/bank_billets/#buscar-por-situa%C3%A7%C3%A3o-do-boleto) por `status`: Filtro por período de vencimento a partir de `expire_from` e até data de vencimento `expire_to`

- Adicionado novos parâmetros ao endpoint de filtro de [Boletos](/reference/v1/bank_billets/#buscar-por-cpf-ou-cnpj) por `cnpj_cpf`: Filtro por período de vencimento a partir de `expire_from` e até data de vencimento `expire_to`

- Adicionado novo endpoint de cancelamento coletivo de [Boletos](/reference/v1/bank_billets/#cancelar-boletos):

### 29/11/2017

- Adicionado endpoint de alteração de [Carteiras de cobrança](/reference/v1/bank_billet_accounts/#alterar-carteira-de-cobran%C3%A7a-padr%C3%A3o) para padrão ou deixar de ser padrão

### 24/11/2017

- Adicionado novos parâmetros ao endpoint de criação de [Carnês](/reference/v1/installments/):

- Novos campos para [Desconto](/reference/v1/installments/#discount_type)

- Adicionado novos parâmetros ao endpoint de criação e alteração de [Assinaturas](/reference/v1/customer_subscriptions/):

- Novos campos para [Desconto](/reference/v1/customer_subscriptions/#discount_type)

### 14/11/2017

- Adicionado novos parâmetros ao endpoint de criação e alteração de [Assinaturas](/reference/v1/customer_subscriptions/):

- Novos campos para [Multa](/reference/v1/customer_subscriptions/#fine_type)

- Novos campos para [Juros](/reference/v1/customer_subscriptions/#interest_type)

### 07/11/2017

- Adicionado novos parâmetros ao endpoint de criação de [Carnes](/reference/v1/installments/):

- Novos campos para [Multa](/reference/v1/installments/#fine_type)

- Novos campos para [Juros](/reference/v1/installments/#interest_type)

### 20/09/2017

- Adicionado novos parâmetros ao endpoint de alteração de [Boletos](/reference/v1/bank_billets/#alterar-boleto)

### 09/08/2017

- Adicionado endpoint de alteração de [Boletos](/reference/v1/bank_billets/#alterar-boleto)

### 31/05/2017

- Inclui `notes` nos [Carnês](/reference/v1/installments/)

- Inclui `notes` nas [Assinaturas](/reference/v1/customer_subscriptions/)

### 24/05/2017

- Documentando endpoint para RAW da [Remessa](/reference/v1/remittances/#rawtextplain-do-cnab)

### 23/05/2017

- Inclui `nickname` nos [Clientes](/reference/v1/customers/)

### 22/05/2017

- Adicionado endpoint de pagamento aos [Boletos](/reference/v1/bank_billets/#marcar-boleto-como-pago)

### 18/05/2017

- Inclui eventos `bank_billet_discharge.*` e `bank_billet_remittance.*` na página de [eventos dos webhooks](/webhooks/events/)

### 17/04/2017

- Documenta informações sobre retentativas de entrega de [Webhooks](/webhooks/)

### 17/02/2017

- Documenta eventos de [carnês](/webhooks/events/)

- Inclusão de valor padrão para o campo `cycle` em [Assinaturas](/reference/v1/customer_subscriptions) e [Carnês](/reference/v1/installments)

### 08/02/2017

- Documenta o campo `default` em [Carteira de Cobrança](/reference/v1/bank_billet_accounts/#default)

- Adicionado novo scope para retornar url de [checkout](/authentication/permissions/)

- Adicionado novo scope para [subscription](/authentication/permissions/)

### 06/02/2017

- Incluída informação sobre a [limpeza do ambiente de sandbox](/sandbox/#limpeza-do-ambiente)

### 19/01/2017

- Adicionando novos endpoints aos [Boletos](/reference/v1/bank_billets)

### 13/01/2017

- Atualizando modelo de dados dos [Boletos](/reference/v1/bank_billets)

- Adicionado opções `amount` e `with_fines` ao [Boletos](/reference/v1/bank_billets/#gerar-segunda-via-do-boleto)

### 26/12/2016

- Revisão e atualização dos modelos de dados dos endpoints da API

- Revisão das [Carteiras](/bank_contracts)

### 19/11/2016

- Inclui endpoint de busca por [CPF ou CNPJ](/reference/v1/customers/#buscar-por-cpf-ou-cnpj) nos clientes

- Inclui endpoint de busca por [E-mail](/reference/v1/customers/#buscar-por-e-mail) nos clientes

### 31/10/2016

- Adiciona `bank_billet_layout_id` aos [Boletos](/reference/v1/bank_billets)

### 28/10/2016

- Adiciona `fine_for_delay` e `late_payment_interest` aos [Carnês](/reference/v1/installments)

- Adiciona `fine_for_delay` e `late_payment_interest` às [Assinaturas](/reference/v1/customer_subscriptions)

### 24/10/2016

- Adiciona `bank_billet_ids` a [Remessa](/reference/v1/remittances).

### 12/10/2016

- Melhora a explicação de como o [limite de requisições](/#limite-de-requisi%C3%A7%C3%B5es) é calculado e aumenta o limite por segundo de 1 para 5 requisições.

### 14/09/2016

- Retira a obrigatoriedade do campo `bank_billet_account_id` e documenta a existência da carteira de cobrança padrão.

### 29/08/2016

- Melhora a explicação sobre [status da carteira de cobrança](/reference/v1/bank_billet_accounts/#status).

- Inclui aviso na página de [eventos dos webhooks](/webhooks/events/) de que os eventos `bank_billet_account.homologated` e `bank_billet_account.validated` serão renomeados em breve para `bank_billet_account.homologation_started` e `bank_billet_account.validation_released` respectivamente.

### 15/08/2016

- Inclui endpoint de [Carnês](/reference/v1/installments)

### 10/08/2016

- Corrige campos `amount`, `cycle` e `days_in_advance` da [assinatura](/reference/v1/customer_subscriptions)

### 20/05/2016

- Corrige endpoint de [geração da próxima cobrança da assinatura](/reference/v1/customer_subscriptions#gerar-pr%C3%B3xima-cobran%C3%A7a)

### 18/05/2016

- Inclui endpoint de [Assinaturas](/reference/v1/customer_subscriptions)

### 06/05/2016

- Atualização de [Eventos](/webhooks/events/) e exemplos de [Payload](/webhooks/payloads/)

### 04/05/2016

- Novo endpoint para gerar [segunda via de boletos](/reference/v1/bank_billets/#gerar-segunda-via-do-boleto)

### 03/05/2016

- Inclui 'status' nas informações retornadas nas carteiras de cobrança

- Novo endpoint para homologar carteiras de cobrança

### 24/02/2016

- Padronizando CEP

### 24/12/2015

- Atualiza as informações retornadas nas carteiras (`BankBilletAccount`)

- Inclui dicionário de dados de CNAB Retorno

- Atualiza status faltando no dicionário de dados de CNAB Remessa

- Inclui informações de payload dos webhooks de usuário, CNAB Remessa e CNAB Retorno

### 09/12/2015

- Atualização dos campos obrigatórios dos boletos

- Atualização dos campos obrigatórios dos clientes

- Revisão de todos os códigos de exemplo

### 28/10/2015

- Tabela com lista atual de retornos e remessas disponíveis

### 22/10/2015

- Atualizada lista de carteiras do Itaú

- Atualizada lista de carteiras do Bradesco

- Atualizada lista de carteiras do Banco do Brasil

### 09/10/2015

- Atualizada lista de carteiras do Santander

### 06/10/2015

- Atualiza informações de convênio de remessa

- Atualiza lista de atributos opcionais do boleto

### 30/09/2015

- Atualiza lista de carteiras da Caixa

### 14/09/2015

- Adicionado carteiras do Banestes

### 27/08/2015

- Adicionado endpoint destroy na remessa

### 24/08/2015

- Adicionado campo URL do arquivo de remessa

### 10/08/2015

- Adicionado campo extra3 para uso em remessas

### 23/06/2015

- Adicionado eventos de remessa

- Adicionado eventos de retorno

### 18/06/2015

- Adicionado ID da carteira a documentação de boletos

- Adicionado exemplos a API de Parceiros

### 12/06/2015

- Renomeado endpoint de CNAB de Retorno

- Adicionado endpoint de CNAB de Remessa

### 11/06/2015

- Adicionado endpoint `pay_off` na API de CNAB

- Correção exemplo de cancelamento de boleto

### 17/04/2015

- Adicionado novo scopo `balance`

- Inclusão de account_level na resposta sobre usuários

- Adicionado API de CNAB (Retorno)

- Adicionado endpoints(novo saque, solicitar saque, informações do saque e listagem de saques) na API de transações

- Adicionado novos eventos de webhooks

### 31/03/2015

- Inclusão de carteiras de cobrança.

- Correções nos exemplos em Bash do endpoint de Clientes

- Adicionado opção de usar PUT para cancelar Boletos

### 08/03/2015

- As notificações antigas ficaram obsoletas e não devem ser mais utilizadas. Para receber notificações sobre os eventos que ocorrem no sistema é necessário usar os Webhooks.

### 16/02/2015

- O código do status (`BankBillet#status`) de um boleto vencido mudou de `due` para `overdue`.
