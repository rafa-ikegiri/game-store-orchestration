# FIAP Cloud Games - Tech Challenge Fase 2

## Sobre o Projeto

A FIAP Cloud Games (FCG) é uma plataforma para gerenciamento e compra de jogos digitais.

Nesta fase do Tech Challenge, a aplicação foi evoluída de uma arquitetura monolítica para uma arquitetura de microsserviços orientada a eventos utilizando RabbitMQ.

## Arquitetura

A solução é composta pelos seguintes microsserviços:

- UsersAPI
- CatalogAPI
- PaymentsAPI
- NotificationsAPI

Infraestrutura:

- SQL Server
- RabbitMQ
- Docker
- Kubernetes

## Repositórios

- UsersAPI
- CatalogAPI
- PaymentsAPI
- NotificationsAPI
- game-store-orchestration

## Fluxo de Cadastro

UsersAPI
↓
UserCreatedEvent
↓
RabbitMQ
↓
NotificationsAPI
↓
E-mail de boas-vindas

## Fluxo de Compra

CatalogAPI
↓
OrderPlacedEvent
↓
RabbitMQ
↓
PaymentsAPI
↓
PaymentProcessedEvent
↓
RabbitMQ
↓
CatalogAPI

e

RabbitMQ
↓
NotificationsAPI

## Estrutura

--- ### 8. Docker Compose ```markdown ## Executando com Docker Compose ```bash docker-compose up -d
--- ### 9. Kubernetes ```markdown ## Deploy no Kubernetes ```bash kubectl apply -f k8s/

kubectl get pods
kubectl get deployments
kubectl get services

--- ### 10. Tecnologias ```markdown ## Tecnologias - .NET 8 - ASP.NET Core - Entity Framework Core - SQL Server - RabbitMQ - Docker - Docker Compose - Kubernetes - JWT - FluentValidation - Serilog

## Fluxos Validados

✅ Cadastro de usuário

✅ UserCreatedEvent

✅ Compra de jogo

✅ OrderPlacedEvent

✅ PaymentProcessedEvent

✅ Notificações

✅ Kubernetes

✅ Docker Compose
