# Arquitetura da Clínica Vida+

## O caminho de uma requisição

​```mermaid
sequenceDiagram
    participant N as Navegador do paciente
    participant D as Servidor DNS
    participant S as Servidor da Clínica Vida+
    N->>D: uninove.br?
    D-->>N: 167.99.0.217
    N->>S: conexão TCP e TLS na porta 443
    N->>S: GET /consultas/agendar
    S-->>N: 200 OK, HTML da agenda
​```

## Evidência do DNS

​```
Server:		127.0.0.53
Address:	127.0.0.53#53

Non-authoritative answer:
Name:	uninove.br
Address: 167.99.0.217
​```

## Evidência do HTTP

| Método | Recurso | Status |
| ------ | ------- | ------ |
| GET | `widget-Cyr_pu2y.css` | 200 |
| GET | `wa/?medium=fetch&fmt=g` | 204 |
| GET | `1112678700/?random=1946...` | 302 |
| XHR | `conversations?website_token=...` | 304 |

## Por que o formulário de agendamento precisa de HTTPS

O formulário de agendamento da Clínica Vida+ vai coletar dados sensíveis do paciente, como CPF e telefone, para confirmar a identidade e o contato do agendamento. Sem HTTPS, essas informações trafegam em texto puro pela rede, podendo ser interceptadas por qualquer pessoa no mesmo caminho da conexão, como em uma rede Wi-Fi pública. O HTTPS criptografa a comunicação entre o navegador e o servidor, impedindo que terceiros leiam ou alterem os dados durante o envio. Além disso, expor CPF e telefone sem proteção viola princípios da LGPD, já que são dados pessoais que exigem tratamento seguro. Por isso, o uso de HTTPS é indispensável para garantir a confidencialidade e a integridade dessas informações.