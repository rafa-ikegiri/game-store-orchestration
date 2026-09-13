# FIAP Cloud Games - Tech Challenge Fase 3

## 📋 Sobre o Projeto

A FIAP Cloud Games (FCG) é uma plataforma para gerenciamento e compra de jogos digitais baseada em microsserviços. 

Nesta **Fase 3** do Tech Challenge, a arquitetura foi evoluída para resolver desafios críticos de **exposição segura de serviços, visibilidade sistêmica, otimização de recursos ociosos e alta performance**, implementando:
1. **API Gateway (Kong):** Ponto de entrada unificado, roteamento e validação de tokens JWT.
2. **Arquitetura Serverless (NotificationsAPI):** Migração do microsserviço de notificações para um modelo reativo acionado por mensageria, eliminando containers ociosos 24/7.
3. **Stack de Observabilidade (Prometheus & Grafana):** Coleta de métricas nativas OpenTelemetry/ASP.NET Core e dashboards em tempo real (**Latência, Throughput e Erros**).
4. **Persistência Poliglota e Cache Distribuído:** Integração com **MongoDB** (para dados flexíveis/avaliações) e **Redis** (para cache de alta performance), acompanhado do **Redis Insight** para monitoramento visual.

---

# 🏗️ Arquitetura e Componentes

A solução é composta pelos seguintes microsserviços e serviços de infraestrutura:

- **Kong API Gateway:** Gateway de borda / Ponto de entrada único
- **UsersAPI:** Gestão de usuários, autenticação e JWT (.NET)
- **CatalogAPI:** Gestão do catálogo, cache, NoSQL e início de compras (.NET)
- **PaymentsAPI:** Processamento de pagamentos (.NET)
- **NotificationsAPI (Serverless):** Envio de notificações orientadas a eventos
- **SQL Server:** Bancos relacionais transacionais
- **MongoDB:** Banco NoSQL para alta volumetria / dados flexíveis
- **Redis & Redis Insight:** Camada de cache distribuído e interface visual
- **RabbitMQ:** Barramento de mensageria assíncrona
- **Prometheus & Grafana:** Stack de observabilidade e métricas

---

# 🔗 Repositórios

## Microsserviços

- UsersAPI: https://github.com/rafa-ikegiri/UsersAPI
- CatalogAPI: https://github.com/rafa-ikegiri/CatalogAPI
- PaymentsAPI: https://github.com/rafa-ikegiri/PaymentsAPI
- NotificationsAPI: https://github.com/rafa-ikegiri/NotificationsAPI

## Infraestrutura e Orquestração

- game-store-orchestration: https://github.com/rafa-ikegiri/game-store-orchestration

---

# 🔗 Portas e Endereços Úteis (Endpoints)

| Serviço | Porta / URL Local | Descrição |
| :--- | :--- | :--- |
| **API Gateway (Kong Proxy)** | `http://localhost:8000` | Ponto de entrada único para o cliente |
| **Kong Admin API** | `http://localhost:8001` | Gerenciamento de rotas e plugins do Kong |
| **Grafana (Observabilidade)** | `http://localhost:3000` | Dashboards em tempo real (`admin` / `admin`) |
| **Prometheus** | `http://localhost:9090` | Coleta de métricas e targets |
| **Redis Insight (Cache UI)** | `http://localhost:5540` | Interface visual para monitoramento do cache Redis |
| **RabbitMQ Management** | `http://localhost:15672` | Painel da mensageria (`guest` / `guest`) |
| **CatalogAPI (.NET)** | `http://localhost:5002` | Microsserviço de catálogo e endpoint `/metrics` |
| **UsersAPI (.NET)** | `http://localhost:5001` | Microsserviço de usuários |
| **PaymentsAPI (.NET)** | `http://localhost:5003` | Microsserviço de pagamentos |

---

# 📊 Observabilidade (Prometheus & Grafana)

A instrumentação utiliza as métricas nativas do ASP.NET Core moderno. No **Grafana**, o dashboard da Fase 3 monitora em tempo real:
- **Throughput:** `sum(rate(microsoft_aspnetcore_hosting_http_server_request_duration_count[1m]))`
- **Latência Média:** `sum(rate(microsoft_aspnetcore_hosting_http_server_request_duration_sum[1m])) / sum(rate(microsoft_aspnetcore_hosting_http_server_request_duration_count[1m])) * 1000`
- **Taxa de Erros (4xx/5xx):** `sum(rate(microsoft_aspnetcore_hosting_http_server_request_duration_count{http_response_status_code=~"[45].*"}[1m]))`

---

# 🚀 Executando com Docker Compose

## Pré-requisitos
- Docker Desktop
- Docker Compose

## Executar a solução completa
```bash
docker-compose up -d --build
