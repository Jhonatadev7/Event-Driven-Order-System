# 🛒 Event-Driven Order System

Sistema de pedidos com arquitetura orientada a eventos e padrão Saga para compensação de falhas.

## 🛠 Tecnologias
- Kotlin + Spring Boot 3.2
- Apache Kafka (eventos de domínio)
- PostgreSQL (persistência)

## 📋 Funcionalidades
- Criação de pedido com publicação de evento no Kafka
- Aprovação de pagamento com transição de estado
- Cancelamento com evento de compensação (Saga Pattern)
- Rastreamento de status por cliente

## 🚀 Como rodar

```bash
docker-compose up -d  # Sobe Postgres + Kafka + Zookeeper
./gradlew bootRun
```

## 📡 Endpoints

| Método | Rota | Descrição |
|--------|------|-----------|
| POST | `/api/orders` | Cria pedido |
| PATCH | `/api/orders/{id}/approve` | Aprova pagamento |
| PATCH | `/api/orders/{id}/cancel` | Cancela + compensação |
| GET | `/api/orders/{id}` | Busca pedido |
| GET | `/api/orders/customer/{id}` | Pedidos do cliente |

## 🔄 Saga Pattern

```
CREATED → PAYMENT_PENDING → PAYMENT_APPROVED → SHIPPING → DELIVERED
                ↓ (falha)
            CANCELLED (evento de compensação publicado)
```

---
> Projeto desenvolvido por **Jhonata Breno** — Estudante de ADS | Backend Developer
