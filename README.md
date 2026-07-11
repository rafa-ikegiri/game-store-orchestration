# FIAP Cloud Games - Tech Challenge Fase 2

## 📋 Sobre o Projeto

A FIAP Cloud Games (FCG) é uma plataforma para gerenciamento e compra de jogos digitais.

Nesta fase do Tech Challenge, a aplicação foi evoluída de uma arquitetura monolítica para uma arquitetura baseada em microsserviços orientados a eventos, utilizando RabbitMQ para comunicação assíncrona entre os serviços.

---

# 🏗️ Arquitetura

A solução é composta pelos seguintes microsserviços:

- UsersAPI
- CatalogAPI
- PaymentsAPI
- NotificationsAPI

Além dos serviços de infraestrutura:

- SQL Server
- RabbitMQ
- Docker
- Kubernetes

---

# 🔗 Repositórios

## Microsserviços

- UsersAPI: https://github.com/rafa-ikegiri/UsersAPI
- CatalogAPI: https://github.com/rafa-ikegiri/CatalogAPI
- PaymentsAPI: https://github.com/rafa-ikegiri/PaymentsAPI
- NotificationsAPI: https://github.com/rafa-ikegiri/NotificationsAPI

## Infraestrutura

- game-store-orchestration: https://github.com/rafa-ikegiri/game-store-orchestration

---

# 🧩 Microsserviços

## UsersAPI

Responsável por:

- Cadastro de usuários
- Login
- Geração de JWT
- Autorização baseada em Roles

### Eventos Publicados

- UserCreatedEvent

---

## CatalogAPI

Responsável por:

- CRUD de jogos
- Consulta do catálogo
- Biblioteca de jogos do usuário
- Início do fluxo de compra

### Eventos Publicados

- OrderPlacedEvent

### Eventos Consumidos

- PaymentProcessedEvent

---

## PaymentsAPI

Responsável por:

- Processamento de pagamentos (simulado)

### Eventos Consumidos

- OrderPlacedEvent

### Eventos Publicados

- PaymentProcessedEvent

---

## NotificationsAPI

Responsável por:

- Envio de e-mail de boas-vindas (simulado)
- Envio de confirmação de compra (simulado)

### Eventos Consumidos

- UserCreatedEvent
- PaymentProcessedEvent

---

# 🔄 Fluxos de Negócio

## Cadastro de Usuário

```text
UsersAPI
    ↓
UserCreatedEvent
    ↓
RabbitMQ
    ↓
NotificationsAPI
    ↓
E-mail de boas-vindas
```

---

## Compra de Jogo

```text
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
    ↓
Adiciona o jogo à biblioteca do usuário
```

```text
RabbitMQ
    ↓
NotificationsAPI
    ↓
E-mail de confirmação da compra
```

---

# 🛠️ Tecnologias Utilizadas

- .NET 8
- ASP.NET Core
- Entity Framework Core
- SQL Server
- RabbitMQ
- Docker
- Docker Compose
- Kubernetes
- JWT Authentication
- FluentValidation
- Serilog

---

# 📦 Estrutura do Repositório

```text
game-store-orchestration
│
├── README.md
├── .gitignore
├── docker-compose.yml
│
└── k8s
    ├── rabbitmq
    │   ├── deployment.yaml
    │   ├── service.yaml
    │   └── secret.yaml
    │
    ├── sqlserver
    │   ├── deployment.yaml
    │   ├── service.yaml
    │   └── secret.yaml
    │
    ├── users-api
    │   ├── deployment.yaml
    │   ├── service.yaml
    │   ├── configmap.yaml
    │   └── secret.yaml
    │
    ├── catalog-api
    │   ├── deployment.yaml
    │   ├── service.yaml
    │   ├── configmap.yaml
    │   └── secret.yaml
    │
    ├── payments-api
    │   ├── deployment.yaml
    │   ├── service.yaml
    │   ├── configmap.yaml
    │   └── secret.yaml
    │
    └── notifications-api
        ├── deployment.yaml
        ├── service.yaml
        ├── configmap.yaml
        └── secret.yaml
```

---

# ☸️ Recursos Kubernetes

A infraestrutura Kubernetes da solução utiliza:

- Deployments
- Services
- ConfigMaps
- Secrets

Todos os manifestos Kubernetes foram centralizados neste repositório para facilitar a implantação e manutenção da aplicação.

---

# 🚀 Executando com Docker Compose

## Pré-requisitos

- Docker Desktop
- Docker Compose

## Executar a solução

```bash
docker-compose up -d
```

## Verificar os containers

```bash
docker ps
```

---

# ☸️ Deploy no Kubernetes

## Pré-requisitos

- Docker Desktop Kubernetes habilitado
- kubectl

## Aplicar os manifestos

```bash
kubectl apply -f k8s/
```

## Verificar os recursos

### Deployments

```bash
kubectl get deployments
```

### Services

```bash
kubectl get services
```

### Pods

```bash
kubectl get pods
```

---

# 🔐 ConfigMaps e Secrets

## ConfigMaps

Utilizados para armazenar configurações não sensíveis:

- Ambiente da aplicação
- Host do RabbitMQ
- Configurações gerais

## Secrets

Utilizados para armazenar informações sensíveis:

- Senha do SQL Server
- Connection Strings
- Chave JWT
- Credenciais do RabbitMQ

---

# 🗄️ Banco de Dados

O ambiente utiliza SQL Server como banco de dados principal.

### Bases de Dados

- UsersDb
- CatalogDb
- PaymentsDb

As tabelas são criadas através de migrations do Entity Framework Core.

---

# 📨 Mensageria

Broker utilizado:

- RabbitMQ

Eventos implementados:

- UserCreatedEvent
- OrderPlacedEvent
- PaymentProcessedEvent

---

# ✅ Funcionalidades Validadas

## Cadastro de Usuário

- Usuário cadastrado com sucesso
- UserCreatedEvent publicado
- NotificationsAPI consumiu o evento
- E-mail de boas-vindas enviado

## Compra de Jogo

- OrderPlacedEvent publicado
- PaymentsAPI processou o pagamento
- PaymentProcessedEvent publicado
- CatalogAPI atualizou a biblioteca do usuário
- NotificationsAPI enviou confirmação da compra

---

# 📹 Demonstração

Durante a apresentação serão demonstrados:

- Estrutura dos microsserviços
- Execução com Docker Compose
- RabbitMQ
- SQL Server
- Kubernetes
- Deployments
- Services
- ConfigMaps
- Secrets
- Fluxo de cadastro
- Fluxo de compra
- Consumo dos eventos
- Logs dos consumidores

---

# 👨‍💻 Autor

Rafael Ikegiri Cardoso

Tech Challenge - FIAP Cloud Games
