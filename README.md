# Projeto de Estudo: Pedidos com RabbitMQ e Spring Boot

Este projeto foi inspirado em um desafio técnico, mas o objetivo principal foi aprender e praticar o uso do RabbitMQ em conjunto com Spring Boot e MongoDB, simulando o fluxo de processamento de pedidos em um ambiente de mensageria.

##  fluxo da Aplicação

1.  Um pedido (mensagem JSON) é publicado em uma fila do **RabbitMQ**.
2.  O microsserviço **Spring Boot** consome a mensagem.
3.  O serviço processa os dados, calcula o valor total e salva o pedido no **MongoDB**.
4.  Uma **API REST** expõe endpoints para consultar os dados salvos.

## 🛠️ Tecnologias

-   **Linguagem:** Java 21
-   **Framework:** Spring Boot 3.5.5 (Web, AMQP, Data MongoDB)
-   **Mensageria:** RabbitMQ (via Docker Compose)
-   **Banco de Dados:** MongoDB (via Docker Compose)
-   **Containerização:** Docker 

## 🚀 Como Executar

1.  Clone o repositório:
    ```bash
    https://github.com/vcfernandes/Btgpactual-RabbitMq
    cd Btgpactual-RabbitMq-main
    ```

2.  Suba os containers:
    ```bash
    docker-compose up -d
    ```
    -   **API** estará disponível em `http://localhost:8080`.
    -   **RabbitMQ UI** em `http://localhost:15672` (login: `guest`/`guest`).

## 🧪 Como Testar

**1. Publique uma mensagem na fila do RabbitMQ**
**2. Consulta a API

Endpoint: GET /customers/{customerID}/orders

Acesse a UI do RabbitMQ, encontre a fila de pedidos e publique uma mensagem com o payload abaixo:

```json
{
   "codigoPedido": 1001,
   "codigoCliente": 1,
   "itens": [
       {"produto": "lápis", "quantidade": 100, "preco": 1.10},
       {"produto": "caderno", "quantidade": 10, "preco": 1.00}
   ]
}

Exemplo de Resposta no Insominia ou Postman com mais de um pedido:
    
{
  "summary": {
    "totalOnOrders": 2850.00
  },
  "data": [
    {
      "orderId": 1001,
      "customerId": 1,
      "total": 120.00
    },
    {
      "orderId": 1002,
      "customerId": 1,
      "total": 2730.00
    }
  ],
  "pagination": {
    "page": 0,
    "pageSize": 10,
    "totalElements": 2,
    "totalPages": 1
  }
}

  
