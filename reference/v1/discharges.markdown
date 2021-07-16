---
title: CNAB (Retorno)
position: 7
layout: pt
en: "/en/references"
breadcrumb: CNAB (Retorno)
---

## CNAB (Retorno)

| Recurso                  | Descrição
| ------------------------ | ------------------------
| [POST /api/v1/discharges](#enviar-cnab) | Enviar CNAB
| [GET /api/v1/discharges/:id](#informações-do-cnab) | Informações do CNAB
| [GET /api/v1/discharges](#listar-cnabs) | Listar CNABs
| [PUT /api/v1/discharges/:id/pay_off](#quitar-boletos) | Quitar boletos
| [PUT /api/v1/discharges/:id/reprocess](#reprocessar-cnab) | Reprocessar CNAB
| [GET /api/v1/discharges/:id/download](#download-do-cnab) | Download do CNAB

### Modelo de Dados

| Parâmetro              | Obrigatório  | Tipo    | Tamanho | Descrição
| ---------------------- | ----- | ------- | ------- | ------------------------
| **id**                 | N/A   | Integer |         | ID do CNAB
| **file**               | Sim   |         |         | Arquivo
| **content**            | Sim   |         |         | Conteúdo do arquivo
| **filename**           | Não   | String  | 255     | Nome do arquivo
| **status**             | N/A   | String  | 20      | Situação do arquivo ([possíveis valores](#status))
| **processed_at**       | N/A   | DateTime    |         | Data de Processamento
| **created_via_api**    | N/A   | Boolean |         | Enviado pela API
| **bank_billet_account_id**    | Não   | Integer |         | ID da [Carteira de Cobrança](/reference/v1/bank_billet_accounts/)
| **created_via_integration**        | Não   | DateTime    |         | Data de recebimento automático do banco
| **bank_billet_discharges**         | N/A   | Array   |         | Retornos bancários

### Dicionário de Dados

#### status

| unprocessed | Pendente
| processed   | Processado

### Enviar CNAB

`POST /api/v1/discharges`

#### Exemplo de requisição inválida

<ul class="nav nav-tabs" role="tablist">
  <li class="active"><a href="#bash" role="tab" data-toggle="tab">Bash</a></li>
  <!-- <li><a href="#ruby" role="tab" data-toggle="tab">Ruby</a></li> -->
  <!-- <li><a href="#php" role="tab" data-toggle="tab">PHP</a></li> -->
</ul>

<div class="tab-content">
  <div class="tab-pane active" id="bash">
    <small>Requisição:</small>

<pre class="bash">
curl -i \
-H "Authorization: Bearer $BOLETOSIMPLES_TOKEN" \
-H 'Content-Type: multipart/form-data' \
-H 'User-Agent: MyApp (myapp@example.com)' \
-X POST 'https://sandbox.boletosimples.com.br/api/v1/discharges'
</pre>

    <small>Resposta:</small>

<pre class="http">
HTTP/1.1 422 Unprocessable Entity
Server: Cowboy
Connection: keep-alive
Strict-Transport-Security: max-age=2592000
Content-Type: application/json; charset=utf-8
...

{"errors":{"discharge":["não pode ficar em branco"]}}
</pre>
  </div>
  <!-- <div class="tab-pane" id="ruby">
    <small>Requisição:</small>

<pre class="ruby">
@bank_billet_account = BoletoSimples::BankBilletAccount.create({bank_contract_slug: 'sicoob-02'})
if @bank_billet_account.persisted?
  puts "Sucesso :)"
  ap @bank_billet_account.attributes
else
  puts "Erro :("
  ap @bank_billet_account.response_errors
end
</pre>

    <small>Resposta:</small>

<pre class="ruby">
Erro :(
{
     :agency_number => [
        [0] "não pode ficar em branco"
    ],
    :account_number => [
        [0] "não pode ficar em branco"
    ]
}
</pre>

  </div> -->
    <!-- <div class="tab-pane" id="php">
      <small>Requisição:</small>

<pre class="php">
$bank_billet_account = BoletoSimples\bank_billet_account::create(['person_name' => 'Joao da Silva']);
if($bank_billet_account->isPersisted()) {
  echo "Sucesso :)\n";
  print_r($bank_billet_account->attributes());
} else {
  echo "Erro :(\n";
  print_r($bank_billet_account->response_errors);
}
</pre>

      <small>Resposta:</small>

<pre class="php">
Erro :(
Array
(
    [cnpj_cpf] => Array
        (
            [0] => não pode ficar em branco
        )

    [zipcode] => Array
        (
            [0] => não pode ficar em branco
        )

)
</pre>

    </div> -->
</div>

#### Exemplo de requisição válida

<ul class="nav nav-tabs" role="tablist">
  <li class="active"><a href="#bash2" role="tab" data-toggle="tab">Bash</a></li>
  <!-- <li><a href="#ruby2" role="tab" data-toggle="tab">Ruby</a></li> -->
  <!-- <li><a href="#php2" role="tab" data-toggle="tab">PHP</a></li> -->
</ul>

<div class="tab-content">
  <div class="tab-pane active" id="bash2">
    <small>Requisição:</small>

<pre class="bash">
curl -i \
-H "Authorization: Bearer $BOLETOSIMPLES_TOKEN" \
-H 'Content-Type: multipart/form-data' \
-H 'User-Agent: MyApp (myapp@example.com)' \
-F "discharge[file]=@cnab240.ret" \
-X POST 'https://sandbox.boletosimples.com.br/api/v1/discharges'
</pre>

    <small>Resposta:</small>

<pre class="http">
HTTP/1.1 201 Created
Server: Cowboy
Connection: keep-alive
Strict-Transport-Security: max-age=2592000
Location: https://sandbox.boletosimples.com.br/api/v1/discharges/1
Content-Type: application/json; charset=utf-8
...

{
  "id":1,
  "filename":"cnab240.ret",
  "processed_at":"2015-06-11T10:41:41.916-03:00",
  "created_via_api":true,
  "status":"unprocessed"
}
</pre>
  </div>
  <!-- <div class="tab-pane" id="ruby2">
    <small>Requisição:</small>

<pre class="ruby">
@bank_billet_account = BoletoSimples::BankBilletAccount.create({
  bank_contract_slug: 'sicoob-02',
  next_our_number: '1',
  agency_number: '4327',
  agency_digit: '3',
  account_number: '3666',
  account_digit: '8',
  extra1: '1234567'
})
if @bank_billet_account.persisted?
  puts "Sucesso :)"
  ap @bank_billet_account.attributes
else
  puts "Erro :("
  ap @bank_billet_account.response_errors
end
</pre>
  <small>Resposta:</small>

<pre class="ruby">
Sucesso :)
{
    "bank_contract_slug" => "sicoob-02",
       "next_our_number" => "0000001",
         "agency_number" => "4327",
          "agency_digit" => "3",
        "account_number" => "00003666",
         "account_digit" => "8",
         "extra1_length" => "1234567",
                    "id" => 2,
                "extra1" => "1234567",
          "extra1_digit" => nil,
                "extra2" => nil,
          "extra2_digit" => nil
}
</pre>
  </div> -->
  <!-- <div class="tab-pane" id="php2">
    <small>Requisição:</small>

<pre class="php">
$bank_billet_account = BoletoSimples\bank_billet_account::create([
  'person_name' => "Joao da Silva",
  'cnpj_cpf' => "860.196.915-19",
  'email' => "carteira@example.com",
  'address' => "Rua quinhentos",
  'city_name' => "Rio de Janeiro",
  'state' => "RJ",
  'neighborhood' => "bairro",
  'zipcode' => "12312-123",
  'address_number' => "111",
  'address_complement' => "Sala 4",
  'phone_number' => "2112123434"
]);
if($bank_billet_account->isPersisted()) {
  echo "Sucesso :)\n";
  print_r($bank_billet_account->attributes());
} else {
  echo "Erro :(\n";
  print_r($bank_billet_account->response_errors);
}
</pre>
  <small>Resposta:</small>

<pre class="php">
Sucesso :)
Array
(
    [id] => 66
    [city_name] => Rio de Janeiro
    [person_name] => Joao da Silva
    [address] => Rua quinhentos
    [address_complement] => Sala 4
    [address_number] => 111
    [mobile_number] =>
    [cnpj_cpf] => 860.196.915-19
    [email] => carteira@example.com
    [neighborhood] => bairro
    [person_type] => individual
    [phone_number] => 2112123434
    [zipcode] => 12312-123
    [mobile_local_code] =>
    [state] => RJ
    [created_via_api] => 1
)
</pre>
  </div> -->
</div>

### Informações do CNAB

`GET /api/v1/discharges/:id`

#### Exemplo

<ul class="nav nav-tabs" role="tablist">
  <li class="active"><a href="#bash3" role="tab" data-toggle="tab">Bash</a></li>
  <li><a href="#ruby3" role="tab" data-toggle="tab">Ruby</a></li>
  <!-- <li><a href="#php3" role="tab" data-toggle="tab">PHP</a></li> -->
</ul>

<div class="tab-content">
  <div class="tab-pane active" id="bash3">
    <small>Requisição:</small>

<pre class="bash">
curl -i \
-H "Authorization: Bearer $BOLETOSIMPLES_TOKEN" \
-H 'Content-Type: application/json' \
-H 'User-Agent: MyApp (myapp@example.com)' \
-X GET 'https://sandbox.boletosimples.com.br/api/v1/discharges/1'
</pre>

    <small>Resposta:</small>

<pre class="http">
HTTP/1.1 200 OK
Server: Cowboy
Connection: keep-alive
Strict-Transport-Security: max-age=2592000
Content-Type: application/json; charset=utf-8
...

{
  "id": 1,
  "filename": "1804191.RET",
  "processed_at": "2018-04-19",
  "created_via_api": false,
  "status": "processed",
  "bank_billet_account_id": 1,
  "created_via_integration": "2018-04-19T03:03:06-03:00",
  "bank_billet_discharges": [
    {
      "id": 1,
      "occurrence": "06",
      "date_of_occurrence": "2018-04-18",
      "discharge_id": 1,
      "bank_billet_id": 1,
      "occurrence_error": "0000000004",
      "line_parsed": {
        "iof": "0",
        "line_t": "7560001300007T 0604327000000000366680000070439401014     100000000007043920042018000000000014000341056140                         091000010759039984                    00000000000000000000002200000000004                 ",
        "line_u": "7560001300008U 060000000000000000000000000000000000000000000000000000000000000000000000140000000000000140000000000000000000000000000000001804201819042018    00000000000000000000000                              75600000000000000000000       ",
        "paid_at": "2018-04-18",
        "discount": "0",
        "bank_rate": "220",
        "credit_at": "2018-04-19",
        "error_code": "0000000004",
        "event_type": "06",
        "our_number": "00704394",
        "billet_fine": "0",
        "other_fines": "0",
        "paid_amount": "14000",
        "other_credit": "0",
        "value_rebate": "0",
        "agency_number": "4327",
        "credit_amount": "14000",
        "account_number": "00003666",
        "banco_recebedor": "341",
        "agencia_recebedora": "05614",
        "processed_our_number_raw": "00704394"
      },
      "processed_at": "2018-04-19",
      "occurrence_detail": "Liquidação Normal",
      "occurrence_error_detail": "756 - 06 - 0000000004 - Não Reconhecido"
    },
    {
      "id": 2,
      "occurrence": "06",
      "date_of_occurrence": "2018-04-18",
      "discharge_id": 1,
      "bank_billet_id": 2,
      "occurrence_error": "0000000004",
      "line_parsed": {
        "iof": "0",
        "line_t": "7560001300005T 0604327000000000366680000070424401014     100000000007042419042018000000000005000341032120                         092027613530000161                            00000000000000000000002200000000004                 ",
        "line_u": "7560001300006U 060000000000000000000000000000000000000000000000000000000000000000000000050000000000000050000000000000000000000000000000001804201819042018    00000000000000000000000                              75600000000000000000000       ",
        "paid_at": "2018-04-18",
        "discount": "0",
        "bank_rate": "220",
        "credit_at": "2018-04-19",
        "error_code": "0000000004",
        "event_type": "06",
        "our_number": "00704244",
        "billet_fine": "0",
        "other_fines": "0",
        "paid_amount": "5000",
        "other_credit": "0",
        "value_rebate": "0",
        "agency_number": "4327",
        "credit_amount": "5000",
        "account_number": "00003666",
        "banco_recebedor": "341",
        "agencia_recebedora": "03212",
        "processed_our_number_raw": "00704244"
      },
      "processed_at": "2018-04-19",
      "occurrence_detail": "Liquidação Normal",
      "occurrence_error_detail": "756 - 06 - 0000000004 - Não Reconhecido"
    },
    {
      "id": 3,
      "occurrence": "06",
      "date_of_occurrence": "2018-04-18",
      "discharge_id": 1,
      "bank_billet_id": 3,
      "occurrence_error": "0000000004",
      "line_parsed": {
        "iof": "0",
        "line_t": "7560001300003T 0604327000000000366680000070417201014     100000000007041718042018000000000041233001037960                         091000022126830225                  00000000000000000000002200000000004                 ",
        "line_u": "7560001300004U 060000000000000000000000000000000000000000000000000000000000000000000000412330000000000412330000000000000000000000000000001804201819042018    00000000000000000000000                              75600000000000000000000       ",
        "paid_at": "2018-04-18",
        "discount": "0",
        "bank_rate": "220",
        "credit_at": "2018-04-19",
        "error_code": "0000000004",
        "event_type": "06",
        "our_number": "00704172",
        "billet_fine": "0",
        "other_fines": "0",
        "paid_amount": "41233",
        "other_credit": "0",
        "value_rebate": "0",
        "agency_number": "4327",
        "credit_amount": "41233",
        "account_number": "00003666",
        "banco_recebedor": "001",
        "agencia_recebedora": "03796",
        "processed_our_number_raw": "00704172"
      },
      "processed_at": "2018-04-19",
      "occurrence_detail": "Liquidação Normal",
      "occurrence_error_detail": "756 - 06 - 0000000004 - Não Reconhecido"
    },
    {
      "id": 4,
      "occurrence": "02",
      "date_of_occurrence": "2018-04-18",
      "discharge_id": 1,
      "bank_billet_id": 4,
      "occurrence_error": "",
      "line_parsed": {
        "iof": "0",
        "line_t": "7560001300001T 0204327000000000366680000070439401014     100000000007043920042018000000000014000756043270                         091000010759039984                    0000000000000000000000020                           ",
        "line_u": "7560001300002U 020000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000001804201800000000    00000000000000000000000                              75600000000000000000000       ",
        "paid_at": "2018-04-18",
        "discount": "0",
        "bank_rate": "20",
        "credit_at": null,
        "error_code": "",
        "event_type": "02",
        "our_number": "00704394",
        "billet_fine": "0",
        "other_fines": "0",
        "paid_amount": "0",
        "other_credit": "0",
        "value_rebate": "0",
        "agency_number": "4327",
        "credit_amount": "0",
        "account_number": "00003666",
        "banco_recebedor": "756",
        "agencia_recebedora": "04327",
        "processed_our_number_raw": "00704394"
      },
      "processed_at": "2018-04-19",
      "occurrence_detail": "Confirmação Entrada Título",
      "occurrence_error_detail": null
    }
  ]
}
</pre>
  </div>
  <div class="tab-pane" id="ruby3">
    <small>Requisição:</small>

<pre class="ruby">
@discharge = BoletoSimples::Discharge.find(1)
ap @discharge.attributes
</pre>

    <small>Resposta:</small>

<pre class="ruby">
{
            "id" => 1
            "filename" => "1804191.RET",
            "processed_at" => "2018-04-19",
            "created_via_api" => false,
            "status" => "processed",
            "bank_billet_account_id" => 1,
           "created_via_integration" => "2018-04-19T03:03:06-03:00",
            "bank_billet_discharges" => [
            {
                                 "id" => 1,
                         "occurrence" => "06",
                 "date_of_occurrence" => "2018-04-18",
                       "discharge_id" => 1,
                     "bank_billet_id" => 1,
                   "occurrence_error" => "0000000004",
                        "line_parsed" => {
                                     "iof" => "0",
                                  "line_t" => "7560001300007T 0604327000000000366680000070439401014     100000000007043920042018000000000014000341056140                         091000010759039984                    00000000000000000000002200000000004                 ",
                                  "line_u" => "7560001300008U 060000000000000000000000000000000000000000000000000000000000000000000000140000000000000140000000000000000000000000000000001804201819042018    00000000000000000000000                              75600000000000000000000       ",
                                 "paid_at" => "2018-04-18",
                                "discount" => "0",
                               "bank_rate" => "220",
                               "credit_at" => "2018-04-19",
                              "error_code" => "0000000004",
                              "event_type" => "06",
                              "our_number" => "00704394",
                             "billet_fine" => "0",
                             "other_fines" => "0",
                             "paid_amount" => "14000",
                            "other_credit" => "0",
                            "value_rebate" => "0",
                           "agency_number" => "4327",
                           "credit_amount" => "14000",
                          "account_number" => "00003666",
                         "banco_recebedor" => "341",
                      "agencia_recebedora" => "05614",
                "processed_our_number_raw" => "00704394"
            },
                       "processed_at" => "2018-04-19",
                  "occurrence_detail" => "Liquidação Normal",
            "occurrence_error_detail" => "756 - 06 - 0000000004 - Não Reconhecido"
        },
         {
                                 "id" => 2,
                         "occurrence" => "06",
                 "date_of_occurrence" => "2018-04-18",
                       "discharge_id" => 1,
                     "bank_billet_id" => 2,
                   "occurrence_error" => "0000000004",
                        "line_parsed" => {
                                     "iof" => "0",
                                  "line_t" => "7560001300005T 0604327000000000366680000070424401014     100000000007042419042018000000000005000341032120                         092027613530000161                            00000000000000000000002200000000004                 ",
                                  "line_u" => "7560001300006U 060000000000000000000000000000000000000000000000000000000000000000000000050000000000000050000000000000000000000000000000001804201819042018    00000000000000000000000                              75600000000000000000000       ",
                                 "paid_at" => "2018-04-18",
                                "discount" => "0",
                               "bank_rate" => "220",
                               "credit_at" => "2018-04-19",
                              "error_code" => "0000000004",
                              "event_type" => "06",
                              "our_number" => "00704244",
                             "billet_fine" => "0",
                             "other_fines" => "0",
                             "paid_amount" => "5000",
                            "other_credit" => "0",
                            "value_rebate" => "0",
                           "agency_number" => "4327",
                           "credit_amount" => "5000",
                          "account_number" => "00003666",
                         "banco_recebedor" => "341",
                      "agencia_recebedora" => "03212",
                "processed_our_number_raw" => "00704244"
            },
                       "processed_at" => "2018-04-19",
                  "occurrence_detail" => "Liquidação Normal",
            "occurrence_error_detail" => "756 - 06 - 0000000004 - Não Reconhecido"
        },
        {
                                 "id" => 3,
                         "occurrence" => "06",
                 "date_of_occurrence" => "2018-04-18",
                       "discharge_id" => 1,
                     "bank_billet_id" => 3,
                   "occurrence_error" => "0000000004",
                        "line_parsed" => {
                                     "iof" => "0",
                                  "line_t" => "7560001300003T 0604327000000000366680000070417201014     100000000007041718042018000000000041233001037960                         091000022126830225                  00000000000000000000002200000000004                 ",
                                  "line_u" => "7560001300004U 060000000000000000000000000000000000000000000000000000000000000000000000412330000000000412330000000000000000000000000000001804201819042018    00000000000000000000000                              75600000000000000000000       ",
                                 "paid_at" => "2018-04-18",
                                "discount" => "0",
                               "bank_rate" => "220",
                               "credit_at" => "2018-04-19",
                              "error_code" => "0000000004",
                              "event_type" => "06",
                              "our_number" => "00704172",
                             "billet_fine" => "0",
                             "other_fines" => "0",
                             "paid_amount" => "41233",
                            "other_credit" => "0",
                            "value_rebate" => "0",
                           "agency_number" => "4327",
                           "credit_amount" => "41233",
                          "account_number" => "00003666",
                         "banco_recebedor" => "001",
                      "agencia_recebedora" => "03796",
                "processed_our_number_raw" => "00704172"
            },
                       "processed_at" => "2018-04-19",
                  "occurrence_detail" => "Liquidação Normal",
            "occurrence_error_detail" => "756 - 06 - 0000000004 - Não Reconhecido"
        },
        {
                                 "id" => 4,
                         "occurrence" => "02",
                 "date_of_occurrence" => "2018-04-18",
                       "discharge_id" => 1,
                     "bank_billet_id" => 4,
                   "occurrence_error" => "",
                        "line_parsed" => {
                                     "iof" => "0",
                                  "line_t" => "7560001300001T 0204327000000000366680000070439401014     100000000007043920042018000000000014000756043270                         091000010759039984                    0000000000000000000000020                           ",
                                  "line_u" => "7560001300002U 020000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000001804201800000000    00000000000000000000000                              75600000000000000000000       ",
                                 "paid_at" => "2018-04-18",
                                "discount" => "0",
                               "bank_rate" => "20",
                               "credit_at" => nil,
                              "error_code" => "",
                              "event_type" => "02",
                              "our_number" => "00704394",
                             "billet_fine" => "0",
                             "other_fines" => "0",
                             "paid_amount" => "0",
                            "other_credit" => "0",
                            "value_rebate" => "0",
                           "agency_number" => "4327",
                           "credit_amount" => "0",
                          "account_number" => "00003666",
                         "banco_recebedor" => "756",
                      "agencia_recebedora" => "04327",
                "processed_our_number_raw" => "00704394"
            },
                       "processed_at" => "2018-04-19",
                  "occurrence_detail" => "Confirmação Entrada Título",
            "occurrence_error_detail" => nil
        }
    ],
}
</pre>
  </div>
  <!-- <div class="tab-pane" id="php3">
    <small>Requisição:</small>

<pre class="php">
$bank_billet_account = BoletoSimples\bank_billet_account::find(66);
print_r($bank_billet_account->attributes());
</pre>

    <small>Resposta:</small>

<pre class="php">
Array
(
    [id] => 66
    [city_name] => Rio de Janeiro
    [person_name] => Joao da Silva
    [address] => Rua quinhentos
    [address_complement] => Sala 4
    [address_number] => 111
    [mobile_number] =>
    [cnpj_cpf] => 860.196.915-19
    [email] => carteira@example.com
    [neighborhood] => bairro
    [person_type] => individual
    [phone_number] => 2112123434
    [zipcode] => 12312-123
    [mobile_local_code] =>
    [state] => RJ
    [created_via_api] => 1
)
</pre>
  </div> -->
</div>

### Download do CNAB

`GET /api/v1/discharges/:id/download`

#### Exemplo

<ul class="nav nav-tabs" role="tablist">
  <li class="active"><a href="#bash3" role="tab" data-toggle="tab">Bash</a></li>
</ul>

<div class="tab-content">
  <div class="tab-pane active" id="bash3">
    <small>Requisição:</small>

  <pre class="bash">
  curl -i \
  -H "Authorization: Bearer $BOLETOSIMPLES_TOKEN" \
  -H 'Content-Type: application/json' \
  -H 'User-Agent: MyApp (myapp@example.com)' \
  -X GET 'https://sandbox.boletosimples.com.br/api/v1/discharges/1/download'
  </pre>

      <small>Resposta:</small>

  <pre class="http">
  HTTP/1.1 200 OK
  Server: Cowboy
  Connection: keep-alive
  Strict-Transport-Security: max-age=2592000
  Content-Type: application/octet-stream
  Content-Transfer-Encoding: binary
  ...
  02RETORNO01COBRANCA...
  </pre>

  </div>
</div>

### Listar CNABs

`GET /api/v1/discharges`

<table class='table table-bordered'>
  <thead>
    <tr>
      <th>Parâmetro</th>
      <th data-container="body" data-toggle="tooltip" title="Obrigatório">Obrigatório</th>
      <th>Tipo</th>
      <th>Descrição</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>
        <strong>page </strong>
      </td>
      <td>
        Não
      </td>
      <td>
        Number
      </td>
      <td>
        Número da Página
      </td>
    </tr>

    <tr>
      <td>
        <strong>per_page </strong>
      </td>
      <td>
        Não
      </td>
      <td>
        Number
      </td>
      <td>
        Quantidade de registros por página (Máximo de 50)
      </td>
    </tr>

    <tr>
      <td>
        <strong>bank_billet_account_id </strong>
      </td>
      <td>
        Não
      </td>
      <td>
        Number
      </td>
      <td>
        Filtro por ID da Carteira.
      </td>
    </tr>
  </tbody>
</table>

#### Exemplo

<ul class="nav nav-tabs" role="tablist">
  <li class="active"><a href="#bash6" role="tab" data-toggle="tab">Bash</a></li>
  <!-- <li><a href="#ruby6" role="tab" data-toggle="tab">Ruby</a></li> -->
  <!-- <li><a href="#php6" role="tab" data-toggle="tab">PHP</a></li> -->
</ul>

<div class="tab-content">
  <div class="tab-pane active" id="bash6">
    <small>Requisição:</small>

<pre class="bash">
curl -i \
-H "Authorization: Bearer $BOLETOSIMPLES_TOKEN" \
-H 'Content-Type: application/json' \
-H 'User-Agent: MyApp (myapp@example.com)' \
-X GET "https://sandbox.boletosimples.com.br/api/v1/discharges?page=1&per_page=50"
</pre>

    <small>Resposta:</small>

<pre class="http">
HTTP/1.1 200 OK
Server: Cowboy
Connection: keep-alive
Strict-Transport-Security: max-age=2592000
Total: 1
Content-Type: application/json; charset=utf-8
...

[
  {
    "id":1,
    "filename":"cnab240.ret",
    "processed_at":"2015-06-11T10:41:41.916-03:00",
    "created_via_api":true,
    "status":"processed"
  }
]
</pre>
  </div>
  <!-- <div class="tab-pane" id="ruby6">
    <small>Requisição:</small>

<pre class="ruby">
@discharges = BoletoSimples::BankBilletAccount.all(page: 1, per_page: 2)
puts "Carteiras Retornadas: #{@discharges.count}"
puts "Total: #{BoletoSimples.last_request.total}"
puts "Primeira Página: #{BoletoSimples.last_request.links[:first]}"
puts "Página Anterior: #{BoletoSimples.last_request.links[:prev]}"
puts "Próxima Página: #{BoletoSimples.last_request.links[:next]}"
puts "Última Página: #{BoletoSimples.last_request.links[:last]}"
</pre>

    <small>Resposta:</small>

<pre class="http">
CNABs Retornadas: 3
Total: 3
Primeira Página:
Página Anterior:
Próxima Página: https://sandbox.boletosimples.com.br/api/v1/discharges?page=2&per_page=2
Última Página: https://sandbox.boletosimples.com.br/api/v1/discharges?page=2&per_page=2
</pre>
  </div> -->
  <!-- <div class="tab-pane" id="php6">
    <small>Requisição:</small>

<pre class="php">
$discharges = BoletoSimples\bank_billet_account::all(['page' => 1, 'per_page' => 2]);
echo "CNABs Retornados: " . sizeof($discharges) . "\n";
echo "Total: " . BoletoSimples::$last_request->total . "\n";
echo "Primeira Página: " . BoletoSimples::$last_request->links['first'] . "\n";
echo "Página Anterior: " . BoletoSimples::$last_request->links['prev'] . "\n";
echo "Próxima Página: " . BoletoSimples::$last_request->links['next'] . "\n";
echo "Última Página: " . BoletoSimples::$last_request->links['last'] . "\n";
</pre>

    <small>Resposta:</small>

<pre class="http">
CNABs Retornados: 2
Total: 9
Primeira Página:
Página Anterior:
Próxima Página: https://sandbox.boletosimples.com.br/api/v1/discharges?page=2&per_page=2
Última Página: https://sandbox.boletosimples.com.br/api/v1/discharges?page=5&per_page=2
</pre>
  </div> -->
</div>

### Quitar Boletos

`PUT /api/v1/discharges/:id/pay_off` ou `PATCH /api/v1/discharges/:id/pay_off`

É necessário já ter enviado o CNAB.
Todos os boletos que forem identificados dentro do CNAB serão marcados como PAGO e os <a href="/webhooks">Webhooks</a> serão disparados.

#### Exemplo

<ul class="nav nav-tabs" role="tablist">
  <li class="active"><a href="#bash3" role="tab" data-toggle="tab">Bash</a></li>
  <!-- <li><a href="#ruby3" role="tab" data-toggle="tab">Ruby</a></li> -->
  <!-- <li><a href="#php3" role="tab" data-toggle="tab">PHP</a></li> -->
</ul>

<div class="tab-content">
  <div class="tab-pane active" id="bash3">
    <small>Requisição:</small>

<pre class="bash">
curl -i \
-H "Authorization: Bearer $BOLETOSIMPLES_TOKEN" \
-H 'Content-Type: application/json' \
-H 'User-Agent: MyApp (myapp@example.com)' \
-X PUT 'https://sandbox.boletosimples.com.br/api/v1/discharges/1/pay_off'
</pre>

    <small>Resposta:</small>

<pre class="http">
HTTP/1.1 204 OK
Server: Cowboy
Connection: keep-alive
Strict-Transport-Security: max-age=2592000
Content-Type: application/json; charset=utf-8
...

{
  "id":1,
  "filename":"cnab240.ret",
  "processed_at":"2015-06-11T10:41:41.916-03:00",
  "created_via_api":true,
  "status":"processed"
}
</pre>
  </div>
  <!-- <div class="tab-pane" id="ruby3">
    <small>Requisição:</small>

<pre class="ruby">
@bank_billet_account = BoletoSimples::BankBilletAccount.find(4)
ap @bank_billet_account.attributes
</pre>

    <small>Resposta:</small>

<pre class="ruby">
{
    "bank_contract_slug" => "sicoob-02",
       "next_our_number" => "0000001",
         "agency_number" => "4327",
          "agency_digit" => "3",
        "account_number" => "00003666",
         "account_digit" => "8",
                "extra1" => "1234567",
          "extra1_digit" => nil,
                "extra2" => nil,
          "extra2_digit" => nil,
                    "id" => 3
}
</pre>
  </div> -->
  <!-- <div class="tab-pane" id="php3">
    <small>Requisição:</small>

<pre class="php">
$bank_billet_account = BoletoSimples\bank_billet_account::find(66);
print_r($bank_billet_account->attributes());
</pre>

    <small>Resposta:</small>

<pre class="php">
Array
(
    [id] => 66
    [city_name] => Rio de Janeiro
    [person_name] => Joao da Silva
    [address] => Rua quinhentos
    [address_complement] => Sala 4
    [address_number] => 111
    [mobile_number] =>
    [cnpj_cpf] => 860.196.915-19
    [email] => carteira@example.com
    [neighborhood] => bairro
    [person_type] => individual
    [phone_number] => 2112123434
    [zipcode] => 12312-123
    [mobile_local_code] =>
    [state] => RJ
    [created_via_api] => 1
)
</pre>
  </div> -->
</div>

### Reprocessar CNAB

`PUT /api/v1/discharges/:id/reprocess` ou `PATCH /api/v1/discharges/:id/reprocess`

#### Exemplo

<ul class="nav nav-tabs" role="tablist">
  <li class="active"><a href="#bash3" role="tab" data-toggle="tab">Bash</a></li>
  <!-- <li><a href="#ruby3" role="tab" data-toggle="tab">Ruby</a></li> -->
  <!-- <li><a href="#php3" role="tab" data-toggle="tab">PHP</a></li> -->
</ul>

<div class="tab-content">
  <div class="tab-pane active" id="bash3">
    <small>Requisição:</small>

<pre class="bash">
curl -i \
-H "Authorization: Bearer $BOLETOSIMPLES_TOKEN" \
-H 'Content-Type: application/json' \
-H 'User-Agent: MyApp (myapp@example.com)' \
-X PUT 'https://sandbox.boletosimples.com.br/api/v1/discharges/1/reprocess'
</pre>

    <small>Resposta:</small>

<pre class="http">
HTTP/1.1 204 OK
Server: Cowboy
Connection: keep-alive
Strict-Transport-Security: max-age=2592000
Content-Type: application/json; charset=utf-8
...

{
  "id":1,
  "filename":"cnab240.ret",
  "processed_at":"2015-06-11T10:41:41.916-03:00",
  "created_via_api":true,
  "status":"processed"
}
</pre>
  </div>
  <!-- <div class="tab-pane" id="ruby3">
    <small>Requisição:</small>

<pre class="ruby">
@bank_billet_account = BoletoSimples::BankBilletAccount.find(4)
ap @bank_billet_account.attributes
</pre>

    <small>Resposta:</small>

<pre class="ruby">
{
    "bank_contract_slug" => "sicoob-02",
       "next_our_number" => "0000001",
         "agency_number" => "4327",
          "agency_digit" => "3",
        "account_number" => "00003666",
         "account_digit" => "8",
                "extra1" => "1234567",
          "extra1_digit" => nil,
                "extra2" => nil,
          "extra2_digit" => nil,
                    "id" => 3
}
</pre>
  </div> -->
  <!-- <div class="tab-pane" id="php3">
    <small>Requisição:</small>

<pre class="php">
$bank_billet_account = BoletoSimples\bank_billet_account::find(66);
print_r($bank_billet_account->attributes());
</pre>

    <small>Resposta:</small>

<pre class="php">
Array
(
    [id] => 66
    [city_name] => Rio de Janeiro
    [person_name] => Joao da Silva
    [address] => Rua quinhentos
    [address_complement] => Sala 4
    [address_number] => 111
    [mobile_number] =>
    [cnpj_cpf] => 860.196.915-19
    [email] => carteira@example.com
    [neighborhood] => bairro
    [person_type] => individual
    [phone_number] => 2112123434
    [zipcode] => 12312-123
    [mobile_local_code] =>
    [state] => RJ
    [created_via_api] => 1
)
</pre>
  </div> -->
</div>
